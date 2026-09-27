<div align="center">

  <h1>🛡️ SOC Analysis & Incident Response Methodology</h1>

</div>

---

## 🎯 The Mission

A repeatable procedure for triage, investigation, containment and eradication, based on the
**NIST SP 800-61** Computer Security Incident Handling Guide and adapted for a single-analyst lab.

**Mapping to the NIST lifecycle:**

| This document | NIST phase |
| :--- | :--- |
| Phase 0 | Preparation |
| Phases 1 and 2 | Detection & Analysis |
| Phases 3 and 4 | Containment, Eradication & Recovery |
| Phase 5 | Post-Incident Activity |

Worked examples: the [incident response playbooks](soc-playbooks/), the
[Wazuh SIEM recovery case study](investigations/wazuh-siem-recovery-2026-04/), and the
[TryHackMe *Lookup* write-up](labs/).

---

## 🧰 Phase 0: Preparation

Done before an incident, and the reason the later phases have anything to work with.

*   **Logging sources.** Wazuh agents on Linux hosts and a Windows workstation (file integrity monitoring, auditd, security configuration assessment), pfSense firewall and DNS logs, and SPECTRE wireless telemetry forwarded as RFC 5424 syslog.
*   **Time synchronization.** NTP is redirected to the firewall on untrusted segments, so timestamps across sources can be correlated and normalized to UTC.
*   **Baselines.** Known-good host configuration scored against CIS and USG benchmarks, plus a known-networks allowlist that wireless evil-twin detection depends on.
*   **Playbooks.** Written procedures for the alert types most likely to fire: brute force, phishing, ransomware.
*   **Recovery capability.** Proxmox snapshots, plus Restic encrypted backups to Cloudflare R2 with alerting on every run.

---

## 📌 Phase 1: Alert Triage & Contextualization

Classify the alert and establish context.

1.  **Validate the alert source and fidelity.** Identify the generating rule in Wazuh, pfSense or SPECTRE, and read the rule logic that fired rather than the alert title alone.
2.  **Enrich asset and identity.** Map affected hosts, addresses, services and accounts. Establish asset criticality and what normal looks like for that host.
3.  **Assign severity.** This lab uses Wazuh rule levels as the scale:

    | Wazuh level | Severity | Handling |
    | :--- | :--- | :--- |
    | 15 | Critical | Investigate immediately |
    | 12 to 14 | High | Investigate same day |
    | 7 to 11 | Medium | Queue for investigation |
    | 3 to 6 | Low | Review in batch |
    | 0 to 2 | Informational | No action unless corroborated |

4.  **Reach a triage outcome.** One of three:
    *   **True positive.** Malicious activity. Proceed to Phase 2.
    *   **Benign true positive.** The rule fired correctly, but the activity was authorized (an admin script, a scheduled scan, a known device). Document it so the next analyst does not re-investigate.
    *   **False positive.** The rule logic is wrong. Route to Phase 5 for tuning rather than closing silently.

---

## 🔍 Phase 2: Deep-Dive Investigation

Reconstruct the full activity chain.

1.  **Aggregate and correlate logs.** Query authentication, firewall and DNS sources in Wazuh, then pivot across hosts on shared indicators.
2.  **Extract artifacts.** Record addresses, domains, SHA256 hashes, user agents and encoded command-line arguments.
3.  **Reconstruct the timeline.** Build a timestamped sequence of events, normalized to UTC, covering before, during and after the alert.
4.  **Map to MITRE ATT&CK.** Record the specific technique and its tactic, for example technique **T1059.001** (PowerShell) under the **Execution** tactic, rather than naming tactics alone.

---

## 🚧 Phase 3: Evidence Preservation & Containment

Preserve first, then stop the activity. Containment that destroys evidence cannot be undone.

1.  **Preserve evidence before touching the host.** Snapshot the Proxmox guest, export the relevant log ranges from the SIEM, and hash any suspect files. This happens before isolation and before any deletion.
2.  **Isolate.** Revoke the host's inter-segment access with a deny rule on the firewall, or detach the guest's virtual NIC in Proxmox. Block malicious external addresses and domains at the perimeter.
3.  **Revoke identity.** Disable affected accounts, rotate credentials, and terminate active sessions and tokens.

---

## 🛠️ Phase 4: Eradication & Recovery

Remove the malicious presence and return to a known-good state.

1.  **Eradicate.** Remove malicious binaries, scripts and persistence mechanisms, only after Phase 3 preservation is complete.
2.  **Recover.** Restore from a clean Proxmox snapshot or backup where required, then return the system to service under heightened monitoring.
3.  **Verify.** Re-run the baseline benchmark against the recovered host to confirm it is back to a known-good configuration.

---

## 📝 Phase 5: Post-Incident Activity

Turn the incident into a detection.

1.  **Document.** Finalize the write-up using the standard template: timeline, evidence, root cause, remediation.
2.  **Feed detection engineering.** Write or tune a **Sigma or Wazuh rule** to catch an earlier stage of the observed chain. False positives from Phase 1 land here as tuning work.
3.  **Harden.** Recommend the configuration, patch or policy change that prevents recurrence, and record it as an accepted risk if it is not going to be made.
