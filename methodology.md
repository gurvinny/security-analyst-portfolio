# 🛡️ SOC Analysis & Incident Response Methodology

<div align="center">
  <img src="https://img.shields.io/badge/SOP-Incident_Response-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" />
</div>

This document outlines the standard operating procedure (SOP) followed during lab investigations, CTFs, and real-world alert triage. The methodology is heavily inspired by the **NIST SP 800-61 Rev. 2** Computer Security Incident Handling Guide and adapted for Tier 1 SOC analysis workflows.

---

## 📌 Phase 1: Alert Triage & Preparation
The goal of this phase is to rapidly determine if an alert is a true positive, false positive, or benign true positive, and gather the initial context.

1.  **Validate Alert Source & Type:**
    -   Identify the tool generating the alert (e.g., Splunk, Snort, Windows Defender).
    -   Review the rule logic/signature that triggered.
2.  **Contextualize Entities:**
    -   Identify affected users, hostnames, IP addresses, and specific services.
    -   Determine the asset's criticality and baseline behavior.
3.  **Severity & Scope Assessment:**
    -   Assign an initial severity level based on potential impact (e.g., data exfiltration vs. failed login).
    -   Check for related alerts occurring in the same timeframe.
4.  **Initial Triage Decision:**
    -   Classify the alert (True Positive, False Positive). If a true positive, escalate to the Investigation phase.

---

## 🔍 Phase 2: Investigation & Identification
Once an alert is verified as a true positive, deep-dive analysis begins to uncover the full scope of the incident.

1.  **Log Aggregation (SIEM/Splunk/Elastic):**
    -   Query relevant logs surrounding the event timestamp (Authentication logs, Web Server logs, Endpoint EDR/Sysmon, DNS logs).
2.  **Artifact & IOC Extraction:**
    -   Extract all actionable Indicators of Compromise (IOCs), such as:
        -   Malicious IPs / Domains
        -   File Hashes (MD5, SHA256)
        -   Suspicious User Agents
        -   Command-line arguments
3.  **Timeline Reconstruction:**
    -   Build a chronological timeline of events leading up to, during, and after the alert.
4.  **Attacker Methodology Mapping (MITRE ATT&CK):**
    -   Determine how the attacker gained access (Initial Access) and their objective (Execution, Persistence, Exfiltration).
    -   Hunt for lateral movement across the network.

---

## 🚧 Phase 3: Containment
Rapidly halt the progression of the attack to prevent further damage.

1.  **Short-Term Containment:**
    -   Isolate compromised hosts from the network (physically or logically via VLAN/EDR).
    -   Block malicious external IPs and Domains at the firewall (e.g., pfSense).
2.  **Identity Containment:**
    -   Disable affected user accounts.
    -   Force credential rotations and terminate active sessions.
3.  **Long-Term Containment:**
    -   Apply temporary patches or configuration changes to mitigate the exploited vulnerability until a permanent fix is ready.

---

## 🛠️ Phase 4: Eradication & Recovery
Remove the threat entirely and return systems to normal business operations.

1.  **Eradication:**
    -   Delete malicious files, scripts, and registry keys.
    -   Remove any backdoors or unauthorized accounts created by the attacker.
    -   Remediate the root cause (e.g., patching a vulnerable web application).
2.  **Recovery:**
    -   Restore systems and data from clean backups if necessary.
    -   Bring systems back online in a controlled manner.
    -   Implement heightened monitoring for the affected assets to ensure the attacker does not return.

---

## 📝 Phase 5: Lessons Learned (Post-Incident Activity)
Continuous improvement is critical for maturing security operations.

1.  **Documentation:**
    -   Finalize the incident report detailing the "Who, What, When, Where, Why, and How."
2.  **Detection Engineering Feedback Loop:**
    -   Write or tune custom SIEM queries and **Sigma rules** to detect similar attacks earlier in the kill chain.
    -   Update existing SOC Playbooks with new insights.
3.  **Proactive Hardening:**
    -   Recommend architectural changes or security controls to prevent recurrence.
