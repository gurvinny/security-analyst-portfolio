# Case Study: Wazuh SIEM Recovery & CIS Benchmark Hardening

**Environment:** Self-hosted lab · Proxmox / Ubuntu 24.04 LTS
**Platform:** Wazuh 4.14.4 → 4.14.5 · OpenSearch 2.19.4 → 2.19.5
**Date:** April 24, 2026 · **Duration:** single session (~6 hours)

| CIS Score | Failed Controls | Wazuh Version |
|:---:|:---:|:---:|
| **80.6% → 88.9%** | **54 → 31** | **4.14.4 → 4.14.5** |

> Infrastructure detail in this write-up is deliberately kept at subnet and role level. Host
> addresses, port inventories and service names for other lab systems are omitted.

---

## 1. Executive Summary

End-to-end diagnosis, remediation and hardening of a self-hosted Wazuh SIEM running on a Proxmox
virtual machine. The server had a complete data-pipeline failure: zero log entries visible on the
dashboard, while every service reported healthy. The engagement covered authentication-chain
repair, security role configuration, CIS benchmark hardening, and a version upgrade — all in a
single session.

---

## 2. Environment

**Infrastructure**
- Hypervisor: Proxmox VE with LVM-thin storage
- Network: pfSense firewall with VLAN segmentation; the SIEM sits on the management VLAN
- Server OS: Ubuntu 24.04.4 LTS
- Storage: LVM logical volumes following the CIS-recommended separate-partition layout
- Identity: SSO identity provider managing authentication across lab services

**Wazuh stack**
- Manager, Indexer (OpenSearch) and Dashboard, all 4.14.4 → 4.14.5
- Filebeat as the log shipper between Manager and Indexer
- TLS mutual authentication with an internal CA

---

## 3. Problem Statement

**Symptoms.** The dashboard's security events panel showed zero entries across every time range.
All three core services (`wazuh-manager`, `wazuh-indexer`, `wazuh-dashboard`) reported `active`
under systemd, which is what made the failure non-obvious — nothing was alerting on it.

**Initial hypothesis.** A credential mismatch somewhere in the pipeline. The Wazuh stack has three
distinct authentication boundaries that must all agree:

1. Admin user credentials (OpenSearch security layer)
2. Filebeat service account (`logstash` user)
3. Dashboard service account (`kibanaserver` user)

---

## 4. Investigation & Root Cause Analysis

**Method.** Layered, working from the service layer inward to application authentication:
service health via `systemctl` → direct API testing with `curl` against the indexer → config file
audit across all three components → `filebeat test output` → OpenSearch security audit log →
indexer cluster log.

**Findings.** Four compounding failures, not one:

| Finding | Root cause | Resolution |
|---|---|---|
| Admin auth failure | Hash in `internal_users.yml` matched no known password; `curl` returned `401 Unauthorized` | Reset bcrypt hash, applied via `securityadmin.sh` |
| Filebeat cannot write | `logstash` user had no index-creation permission on `wazuh-*` | Created `wazuh_filebeat_writer` role with CRUD + `create_index` |
| `kibanaserver` auth loop | Dashboard failed every 2.5s — an encrypted keystore was overriding the YAML config with a stale password | Rewrote the keystore entries directly |
| Static role conflict | Custom role name collided with an OpenSearch built-in static role, failing `securityadmin.sh` | Renamed the role, removed orphaned stubs from `roles.yml` |
| Duplicate audit rules | Overlapping rule files made `augenrules --load` fail with "Rule exists" | Consolidated to a single supplemental rules file |

### The critical discovery

The Wazuh dashboard keeps an **encrypted keystore** at
`/etc/wazuh-dashboard/opensearch_dashboards.keystore` that **takes precedence over the plain-text
config file**. Updating `opensearch_dashboards.yml` with the correct password changed nothing —
the dashboard kept authenticating with the stale keystore value, every 2.5 seconds, forever.

Resolving it required manipulating the keystore directly with `opensearch-dashboards-keystore` to
remove and re-add both the username and password entries.

---

## 5. Remediation

**Authentication chain.** New bcrypt hashes (cost factor 12) for the admin and `kibanaserver`
users, applied to the live cluster via `securityadmin.sh`; dashboard keystore entries rewritten;
Filebeat connectivity confirmed with `filebeat test output`; data flow verified by checking
`wazuh-alerts-4.x` index doc counts.

**Security roles.** Created `wazuh_filebeat_writer` with the cluster permissions
(`cluster_monitor`, `cluster_composite_ops`, template and pipeline get/put) and index permissions
(`crud`, `create_index`, `manage`, `indices:admin/create`) needed on `wazuh-*`, `wazuh-alerts-*`
and `wazuh-archives-*`, then mapped the `logstash` backend role to it.

**Restart order matters.** Indexer first (wait for cluster GREEN), then Filebeat, then Manager,
then Dashboard.

---

## 6. CIS Benchmark Hardening

Assessed against the **CIS Ubuntu Linux 24.04 LTS Benchmark v1.0.0** using Wazuh's built-in
Security Configuration Assessment module, which evaluates **279 controls**.

| Metric | Before | After |
|---|---|---|
| CIS score | 80.6% (225/279) | **88.9% (248/279)** |
| Failed controls | 54 | 31 |
| Auditd coverage | Partial (conflicting rules) | Full (consolidated) |
| NTP synchronization | Broken (0 sources) | Active (stratum 2) |
| SSH root login | Enabled (default) | Disabled |
| Firewall | UFW active | UFW with explicit deny rules |

### Controls remediated (23 total)

**Auditd rules (11).** Consolidating to a single rule source and working through the immutable
flag (`-e 2`) workflow brought every auditd control to pass: date/time modification, network
environment changes, user/group modification, DAC permission changes, mount events, session
initiation, login/logout, file deletion, privileged command execution, kernel module load/unload,
and audit tool integrity (`chmod 500` on the auditd binaries).

**System hardening (9).** Unused filesystem kernel modules blacklisted; automatic error reporting
removed; `at` restricted via `/etc/at.allow`; `PermitRootLogin no`; `pam_pwhistory` with
`remember=24` and `enforce_for_root`; journald rotation limits; rsyslog file creation mode `0640`;
`/etc/security/opasswd` set to `600 root:root`; `noexec` on `/tmp`.

**Time synchronization (3).** Installed chrony in place of `systemd-timesyncd`, pointed it at the
lab's pfSense gateway as primary NTP source, and resolved a firewall ACL that was blocking NTP
queries from LAN clients. Verified selected-source sync at stratum 2.

**Firewall (2) and log access (1).** UFW loopback rules and anti-spoof deny rules; explicit
outbound NTP allow; indexer log files corrected to `640` with correct ownership, plus a daily cron
job to maintain permissions across log rotation.

### Accepted exceptions

Nine controls were assessed and **accepted with documented justification** rather than silently
failed:

| ID | Control | Justification |
|---|---|---|
| 35540 | Bootloader password | Mitigated by hypervisor console access controls; physical access required |
| 35531 | `noexec` on `/var/log` | Removed to allow JVM GC log rotation; mitigated by directory permissions |
| 35581 | MTA local-only mode | Postfix is used for alert email delivery; local-only breaks alerting |
| 35589 | `systemd-timesyncd` | Replaced by chrony; the two are mutually exclusive |
| 35710 | journal-upload auth | No remote journal aggregation server in this environment |
| 35720 | rsyslog remote host | This server *is* the aggregation host; forwarding to self loops |
| 35624–35639 | Firewall framework | The benchmark wants nftables, iptables **and** UFW simultaneously — mutually exclusive. UFW active with default-deny. |

---

## 7. Version Upgrade (4.14.4 → 4.14.5)

4.14.5 landed mid-engagement. The upgrade broke on the freshly hardened partition layout, which is
the interesting part:

- The indexer post-install script failed because `/var/log` was mounted `noexec`
- Java GC logging could not initialize — it could not open its own log file
- The earlier `chmod 600` on log files prevented the JVM from writing GC logs
- A systemd `ReadWritePaths` override was **insufficient**, because the JVM's own security manager
  runs before the systemd sandbox applies

Resolved by removing `noexec` from `/var/log` (documented above as an accepted exception),
resetting log permissions to `640` with correct ownership, adding the indexer user to the `syslog`
group for directory traversal, correcting a group ownership on the service defaults file, and
re-applying the OpenSearch security config after the upgrade.

---

## 8. Final Verification

| Component | Before | After |
|---|---|---|
| `wazuh-indexer` | Active | Active |
| `wazuh-manager` | Active | Active |
| `wazuh-dashboard` | Active (0 entries) | Active (live data) |
| `filebeat` | Active (auth failure) | Active |
| `auditd` | Active (conflicting rules) | Active |
| `chrony` | Not installed | Active (synced) |

**Pipeline verified:** 2,852 documents confirmed in the day's alerts index; `filebeat test output`
returned a clean TLS handshake; no `kibanaserver` authentication failures in the indexer log after
the fix; `logstash` index-creation permissions confirmed via the API.

**CIS final results**

| Metric | Value |
|---|---|
| Total controls assessed | 279 |
| Controls passed | 248 |
| Controls failed | 31 |
| — of which intentional exceptions | 9 |
| — true remediable failures | 22 |
| **Final score** | **88.9%** |
| Score improvement | **+8.3 percentage points** |
| Controls remediated | **23** |

A separate, later **USG Level 2** audit (a different control set — 471 rules, aligned to DISA STIG
and NIST 800-53) scored **90.98%**. That figure and its evidence screenshot are in the
[investigation README](./README.md).

---

## 9. Lessons Learned

**Technical**
- Application keystores override configuration files. When a config change has no effect, look for
  an encrypted keystore before you look anywhere else.
- OpenSearch static roles cannot be overridden; custom role names must not collide with built-ins.
- The auditd `-e 2` immutable flag needs a reboot to clear; `auditctl -D` must run before
  `augenrules --load` while rules are unlocked.
- JVM GC logging needs execute permission on its log directory, so `noexec` on `/var/log` is
  incompatible with JVM-based services.
- `systemd` `ReadWritePaths` does not bypass the JVM's own security manager, which runs first.
- CIS firewall-framework controls are mutually exclusive by construction. Picking one fails the
  others, and that is not a finding — it is a decision to document.

**Process**
- Snapshot before major upgrades on hardened systems.
- Upgrade order matters: indexer, filebeat, manager, dashboard.
- Re-apply `securityadmin.sh` after every indexer upgrade.
- Test the impact of removing `noexec` on JVM services *before* hardening `/var/log`.
- Document accepted exceptions with justification **at the time of the decision**, not afterwards.

---

## 10. Recommendations

**Immediate** — extend agent coverage to remaining lab hosts; forward firewall syslog into Wazuh;
move credentials into a secrets manager; snapshot the working hardened state.

**Short term** — configure nftables as primary firewall to close the remaining CIS firewall
controls; stand up a secondary log server for journal-upload; implement Wazuh active-response
rules; configure email alerting for critical severity; integrate SSO with the dashboard.

**Long term** — extend the lab with additional monitored endpoints including a Windows agent;
implement threat intelligence feeds; document standard operating procedures for recurring tasks.

---

*Prepared by @gurvinny · April 2026. Written at the time of the engagement; the certification
goals listed in the original have since been completed.*
