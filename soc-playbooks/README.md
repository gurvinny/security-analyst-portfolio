<div align="center">

  <h1>📘 SOC Incident Response Playbooks</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" alt="Status" />
    <img src="https://img.shields.io/badge/Focus-Incident_Response-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" alt="Focus" />
  </p>
</div>

---

## 🎯 The Mission
This directory acts as the central repository for high-fidelity Incident Response Playbooks, meticulously designed for **SOC Tier 1 / Entry-Level Security Analysts**. These standard operating procedures (SOPs) outline structured investigation, containment, and eradication workflows for common security alerts, guaranteeing actionable guidance and operational readiness.

---

## 🏗️ Playbook Methodology
To maintain an aggressive, professional, and methodical incident response posture, **all playbooks in this repository adhere strictly to a unified, modern SOC structure:**

1. **Hero Section:** Dynamic status badges (Severity, Status, Primary Tool) for immediate contextual awareness.
2. **The Mission:** A concise, one-sentence objective defining the playbook's ultimate goal.
3. **Attack Topology:** A visual Mermaid.js flowchart mapping out the expected threat actor workflow or the required defensive response chain.
4. **Executive Summary:** A high-level table summarizing critical playbook elements.
5. **Incident Timeline:** A structured sequence of events for chronological reconstruction.
6. **The Investigation:** Step-by-step triage processes, utilizing `<details>` and `<summary>` tags for deep-dive log analysis, artifact extraction, and command execution review.
7. **MITRE ATT&CK Mapping:** A clean Markdown table correlating playbook actions against specific adversary tactics and techniques.
8. **Closing (Remediation & Lessons Learned):** Procedures for containment, eradication, and post-incident documentation to fortify future defenses.

---

## 📂 Active Playbook Deployments

### [🚨 Brute Force & Credential Stuffing](brute-force-response.md)
*   **Analyst Focus:** Detection and aggressive response workflows for anomalous authentication activities, including password spraying, credential stuffing, and repeated failed login attempts against critical identity infrastructure.

### [🎣 Phishing Analysis & Remediation](phishing-response.md)
*   **Analyst Focus:** Comprehensive, multi-stage analysis of suspicious emails, encompassing header inspection, URL reputation checks, attachment detonation (sandboxing), and assessing user interaction telemetry.

### [🛑 Ransomware Containment](ransomware-containment-playbook.md)
*   **Analyst Focus:** Immediate triage and critical isolation procedures for suspected ransomware detonations, focusing on rapid containment to severely limit encryption spread and preserve volatile forensic evidence.

---
<div align="center">
  <i>"Speed in response is critical, but accuracy in investigation is paramount."</i>
</div>
