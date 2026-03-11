<div align="center">

  <h1>🛡️ SOC Analysis & Incident Response Methodology</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/SOP-Incident_Response-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" alt="Status" />
  </p>
</div>

---

## 🎯 The Mission
Establish a standardized, high-fidelity Standard Operating Procedure (SOP) for triage, investigation, and eradication, heavily inspired by the **NIST SP 800-61 Rev. 2** Computer Security Incident Handling Guide and optimized for Tier 1 SOC operations.

---

## 📌 Phase 1: Alert Triage & Contextualization
The primary goal is rapid classification (True Positive vs. False Positive) and baseline contextualization of the triggering event.

1.  **Validate Alert Source & Fidelity:**
    *   **Analyst Action:** Identify the generating tool (e.g., Splunk, Snort, EDR).
    *   **Observation:** Review the specific rule logic/signature that generated the alert.
2.  **Asset & Identity Enrichment:**
    *   **Analyst Action:** Map affected users, hostnames, IP addresses, and services.
    *   **Observation:** Determine asset criticality and historical baseline behavior.
3.  **Severity & Scope Assessment:**
    *   **Analyst Action:** Assign an initial severity level based on potential operational impact.
    *   **Observation:** Query for related, temporally proximate alerts on the same host or subnet.

---

## 🔍 Phase 2: Deep-Dive Investigation
Upon validation of a True Positive, comprehensive log analysis begins to unearth the full attack lifecycle.

1.  **Log Aggregation & Correlation:**
    *   **Analyst Action:** Query relevant indices (Authentication, Web Server, Sysmon, DNS) within the SIEM (Splunk/Elastic).
2.  **Artifact Extraction & Enrichment:**
    *   **Analyst Action:** Extract all actionable Indicators of Compromise (IOCs).
    *   **Observation:** Document Malicious IPs, Domains, File Hashes (SHA256), Suspicious User Agents, and encoded command-line arguments.
3.  **Timeline Reconstruction:**
    *   **Analyst Action:** Build a chronological, second-by-second timeline of events leading up to, during, and after the alert execution.
4.  **MITRE ATT&CK Mapping:**
    *   **Analyst Action:** Map attacker behavior to specific Tactics, Techniques, and Procedures (TTPs) (e.g., Initial Access, Execution, Persistence).

---

## 🚧 Phase 3: Immediate Containment
Rapidly halt threat progression to mitigate further operational or data impact.

1.  **Network & Endpoint Isolation:**
    *   **Remediation Strategy:** Isolate compromised hosts logically via EDR or physically. Implement block rules for malicious external IPs/Domains at the perimeter firewall (pfSense).
2.  **Identity Revocation:**
    *   **Remediation Strategy:** Disable affected user accounts, force credential rotations, and aggressively terminate active sessions/tokens.

---

## 🛠️ Phase 4: Eradication & Safe Recovery
Remove all malicious presence and return the environment to a known-good state.

1.  **Threat Eradication:**
    *   **Remediation Strategy:** Delete identified malicious binaries, scripts, and persistence mechanisms (registry keys, scheduled tasks).
2.  **System Recovery:**
    *   **Remediation Strategy:** Restore data from clean, immutable backups if required. Return systems online under heightened monitoring.

---

## 📝 Phase 5: Post-Incident Activity (Lessons Learned)
Drive continuous improvement within the SOC by operationalizing findings from the incident.

1.  **Documentation & Reporting:**
    *   **Analyst Action:** Finalize the incident report detailing the "Who, What, When, Where, Why, and How."
2.  **Detection Engineering Feedback Loop:**
    *   **Remediation Strategy:** Develop or tune custom **Sigma rules** to detect earlier stages of the observed kill chain.
3.  **Proactive Hardening:**
    *   **Remediation Strategy:** Recommend architectural changes, patch deployments, or policy updates to prevent recurrence.
