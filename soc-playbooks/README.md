<div align="center">

  <h1>📘 SOC Incident Response Playbooks</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Status-Active-1F2937?style=for-the-badge&logoColor=60A5FA&borderColor=60A5FA" alt="Status" />
    <img src="https://img.shields.io/badge/Focus-Incident_Response-1F2937?style=for-the-badge&logoColor=60A5FA&borderColor=60A5FA" alt="Focus" />
  </p>
</div>

---

## 🎯 Overview
This directory contains incident response playbooks designed for **SOC Tier 1 / Entry-Level Security Analysts**. These playbooks outline structured investigation and response workflows for common security alerts, providing actionable guidance for triage, containment, and recovery.

---

## 🏗️ Playbook Methodology
To ensure consistent, professional, and effective incident handling, **all playbooks in this repository strictly follow a 6-phase incident response structure** based on NIST guidelines:

1. **Preparation:** Prerequisites for handling the alert (log sources, required access, baseline configurations).
2. **Detection & Alerting:** Identification of the trigger, initial alert details, and preliminary SIEM queries.
3. **Investigation:** Step-by-step triage processes, log analysis, timeline reconstruction, and determining the scope of the incident.
4. **Containment:** Immediate actions required to isolate compromised assets and prevent further lateral movement or data exfiltration.
5. **Eradication & Recovery:** Procedures for removing malicious artifacts, restoring systems to a known good state, and verifying operational integrity.
6. **Post-Incident Activity:** Documentation of lessons learned, updating detection rules, improving defenses, and refining the playbook.

---

## 📂 Current Playbooks

### [🚨 Brute Force Response](brute-force-response.md)
Detection and response workflows for anomalous authentication activities, including password spraying, credential stuffing, and repeated failed login attempts against critical infrastructure.

### [🎣 Phishing Analysis](phishing-response.md)
Comprehensive steps to analyze suspicious emails, including header inspection, attachment detonation (sandboxing), URL reputation checks, and determining user interaction.

### [🛑 Ransomware Containment](ransomware-containment-playbook.md)
Immediate triage and isolation procedures for suspected ransomware infections, focusing on rapid containment to limit encryption spread and preserve forensic evidence.

---
<div align="center">
  <i>"Speed in response is critical, but accuracy in investigation is paramount."</i>
</div>
