# Wazuh SIEM Recovery & CIS Hardening
**Date:** April 24, 2026  
**Duration:** Single session (~6 hours)  
**Environment:** Proxmox / Ubuntu 24.04 LTS / Wazuh 4.14.4 → 4.14.5

---

## Summary
Diagnosed and resolved a complete Wazuh SIEM data pipeline failure 
resulting in zero dashboard entries. Repaired the authentication chain 
across three components, restored live data flow, then hardened the 
server from **83% → 88.9%** on the CIS Ubuntu 24.04 LTS Benchmark 
(24 controls remediated).

---

## Problem
- Dashboard showing **0 security events** despite all services active
- `curl` to OpenSearch port 9200 returning `401 Unauthorized`
- Filebeat connecting successfully but unable to write indices
- Dashboard authenticating every 2.5 seconds and failing

---

## Root Causes Found

| Finding | Root Cause |
|---|---|
| Admin auth failure | bcrypt hash in `internal_users.yml` mismatched |
| Filebeat write failure | `logstash` user had no `create_index` permission on `wazuh-*` indices |
| Dashboard auth loop | Encrypted keystore overriding config file with stale password |
| Static role conflict | Custom role name conflicted with OpenSearch built-in static role |
| Auditd rule failure | Duplicate rule files causing `augenrules --load` to fail |

---

## What I Fixed

### Authentication Chain
- Reset admin and kibanaserver bcrypt hashes (cost factor 12)
- Applied security config to live cluster via `securityadmin.sh`
- Discovered and updated dashboard keystore (`opensearch_dashboards.keystore`)
  overriding the yml config — the critical fix that restored the dashboard

### OpenSearch Security
- Created `wazuh_filebeat_writer` role with `crud`, `create_index`, 
  `manage` permissions on `wazuh-*` index patterns
- Resolved static role naming conflict and YAML duplicate field errors

### CIS Hardening (24 controls)
- **Auditd:** Consolidated conflicting rule files, enabled all audit 
  event categories (time, network, identity, DAC, mounts, sessions, 
  file deletion, privileged commands, kernel modules)
- **Kernel modules:** Blacklisted 14 unused filesystem/network modules 
  (afs, ceph, cifs, exfat, fat, fscache, fuse, gfs2, nfs_common, nfsd, 
  smbfs_common, ext, cramfs, squashfs)
- **SSH:** Disabled `PermitRootLogin`
- **PAM:** Configured `pam_pwhistory` with `remember=24`, `enforce_for_root`
- **NTP:** Installed chrony, synced to pfSense firewall (stratum 2)
- **Firewall:** Configured UFW loopback deny rules for spoofing prevention
- **Audit tools:** Set permissions to 500 (owner execute only)
- **Logging:** Configured journald rotation, rsyslog file creation mode 0640

### Wazuh Upgrade (4.14.4 → 4.14.5)
Upgraded all three components during the session. Encountered and resolved:
- Java GC logging blocked by `noexec` on `/var/log` partition
- `/etc/default/wazuh-indexer` group ownership reset by upgrade
- Re-applied OpenSearch security config post-upgrade

---

## Results

| Metric | Before | After |
|---|---|---|
| Dashboard data | 0 entries | Live alerts flowing |
| CIS Score | 83.0% | 88.9% |
| Controls passing | 225/279 | 248/279 |
| Wazuh version | 4.14.4 | 4.14.5 |
| NTP sync | Broken | Synced (pfSense) |
| Auditd coverage | Partial | Full |

---

## Key Lesson
Application keystores take precedence over config files. When a 
config change has no effect, always check for an encrypted keystore 
(`*.keystore`) that may be overriding it.

---

## Full Case Study
See [`case-study.docx`](./case-study.docx) for the complete write-up 
including investigation methodology, remediation steps, accepted 
exception justifications, and recommendations.

---

## Skills Demonstrated
`Wazuh` `OpenSearch` `SIEM` `Linux` `PAM` `auditd` `UFW` `chrony` 
`pfSense` `Proxmox` `CIS Benchmark` `Incident Response` `Ubuntu 24.04`
