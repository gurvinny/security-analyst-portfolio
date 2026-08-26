<div align="center">

# Security Analyst Portfolio

<p align="center">📍 New York City Metro Area | Security Operations &amp; Threat Analysis</p>

<p align="center">
  <a href="mailto:gurvin240@gmail.com"><img src="https://img.shields.io/badge/Email-Contact_Me-1F2937?style=for-the-badge&logo=gmail&logoColor=60A5FA" alt="Email" /></a>
  <a href="https://www.linkedin.com/in/gurvin-s-6a02b3278/"><img src="https://img.shields.io/badge/LinkedIn-Connect-1F2937?style=for-the-badge&logo=linkedin&logoColor=60A5FA" alt="LinkedIn" /></a>
  <img src="https://img.shields.io/badge/Security%2B_%26_CySA%2B-Certified-success?style=for-the-badge&logo=comptia&logoColor=white" alt="Certified" />
  <img src="https://img.shields.io/badge/Status-Actively_Seeking_Roles-success?style=for-the-badge&logo=target&logoColor=white" alt="Status" />
</p>
</div>

> **Last reviewed:** August 2026.

---

## 🚀 The Mission
CompTIA **Security+** and **CySA+** certified Security Operations analyst focused on high-fidelity detection engineering and automated incident triage. Specialized in **SIEM** operations (**Wazuh** / **Splunk** / Elastic), CIS hardening, and network telemetry analysis to reduce dwell time. Everything here is built and broken in a self-hosted lab, then documented the way a shift handover would need it — evidence attached, decisions justified, and the accepted risks named rather than omitted.

---

## ⚙️ Technical Competencies

| **Category** | **Technologies & Platforms** |
| :--- | :--- |
| **SIEM & Security Monitoring** | ![Wazuh](https://img.shields.io/badge/Wazuh-1F2937?style=flat-square&logo=elasticsearch&logoColor=60A5FA) ![Splunk](https://img.shields.io/badge/Splunk-1F2937?style=flat-square&logo=splunk&logoColor=60A5FA) ![Elastic](https://img.shields.io/badge/Elastic-1F2937?style=flat-square&logo=elasticsearch&logoColor=60A5FA) |
| **Network Traffic Analysis (NTA) & IDS/IPS** | ![Wireshark](https://img.shields.io/badge/Wireshark-1F2937?style=flat-square&logo=wireshark&logoColor=60A5FA) ![pfSense](https://img.shields.io/badge/pfSense-1F2937?style=flat-square&logo=pfsense&logoColor=60A5FA) ![Snort/Suricata](https://img.shields.io/badge/Snort/Suricata-1F2937?style=flat-square&logo=suricata&logoColor=60A5FA) |
| **Detection Engineering & Frameworks** | ![Sigma](https://img.shields.io/badge/Sigma-1F2937?style=flat-square&logo=sigma&logoColor=60A5FA) ![YARA](https://img.shields.io/badge/YARA-1F2937?style=flat-square&logoColor=60A5FA) ![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT&CK-1F2937?style=flat-square&logo=mitre&logoColor=60A5FA) |
| **Endpoint Security** | Endpoint Detection &amp; Response (Wazuh agents) · Malware Triage |
| **Security Orchestration & Scripting** | ![Python](https://img.shields.io/badge/Python-1F2937?style=flat-square&logo=python&logoColor=60A5FA) ![Bash](https://img.shields.io/badge/Bash-1F2937?style=flat-square&logo=gnu-bash&logoColor=60A5FA) ![PowerShell](https://img.shields.io/badge/PowerShell-1F2937?style=flat-square&logo=powershell&logoColor=60A5FA) |
| **Operating Systems** | ![Windows](https://img.shields.io/badge/Windows-1F2937?style=flat-square&logo=windows&logoColor=60A5FA) ![Linux](https://img.shields.io/badge/Linux-1F2937?style=flat-square&logo=linux&logoColor=60A5FA) |

---

## 📜 Certifications & Training

*   ![CompTIA Security+](https://img.shields.io/badge/CompTIA-Security%2B-1F2937?style=flat-square&logo=comptia&logoColor=60A5FA) `Certified`
*   ![CompTIA CySA+](https://img.shields.io/badge/CompTIA-CySA%2B-1F2937?style=flat-square&logo=comptia&logoColor=60A5FA) `Certified`

---

## 🔬 Executive Summary: Featured Deployments

| Project Name | Objective | Primary Tools | Outcome | Link |
| :--- | :--- | :--- | :--- | :--- |
| **Home SOC & Resilient Edge Lab** | SOC Telemetry & Visibility | pfSense, **Wazuh** | Engineered a default-deny, 5-VLAN segmented network on a dedicated edge appliance, with a named noise-suppression ruleset (**SOC_SILENCE**) that keeps the firewall log SIEM-ready. Wazuh ingests agent telemetry from lab hosts; firewall log forwarding is the next integration step. | [View Repo](https://github.com/gurvinny/home-network-lab) |
| **Wazuh SIEM Recovery & Hardening** | Incident Response & Hardening | **Wazuh**, OpenSearch, CIS | Diagnosed a full log-ingestion failure across the OpenSearch authentication chain and restored live alerting, then hardened the host to **88.9%** on the CIS Ubuntu 24.04 benchmark and **90.98%** on the USG Level 2 audit. | [View Case Study](investigations/wazuh-siem-recovery-2026-04/) |
| **Automated Phish Extractor** | Triage Automation | **Python**, VirusTotal, AbuseIPDB | Reduced manual triage latency by automating IOC extraction and threat-intel enrichment, auto-scoring risk and emitting **YARA/Sigma** detections plus standardized **Incident Response** reports. | [View Repo](https://github.com/gurvinny/Automated-Phish-Extractor) |

---

## 🛠️ Analytical Methodology

*   **Framework Alignment:** Mapping all lab detections to **MITRE ATT&CK** tactics (Initial Access, Persistence, Exfiltration).
*   **Incident Lifecycle:** Following **NIST 800-61 r2** for structured Preparation, Detection, and Containment.
*   **Documentation:** Maintaining standardized investigation logs to ensure chain of custody, perform comprehensive **Forensics**, and deliver clear executive reporting.

---

## 📂 SOC Portfolio Modules

### 📘 [Incident Response Playbooks](soc-playbooks/)
Structured standard operating procedures (SOPs) for triage, containment, and eradication.
*   **Analyst Focus:** Phishing Analysis, Ransomware Containment, Brute Force Triage.

### 🔍 [Detection Engineering](detections/)
Vendor-agnostic detection logic written in Sigma and mapped to ATT&CK.
*   **Currently:** one Sigma rule (PowerShell download cradle, T1059.001). This section is early — it grows as lab investigations produce detections worth generalizing.

### 🧪 [Lab Investigations](labs/)
Forensic write-ups reconstructing attacker kill chains and the artifacts each stage leaves behind.
*   **Currently:** one full report (TryHackMe *Lookup* — elFinder RCE → SUID PATH hijack → root), plus the standard write-up template every report follows.

### 🔬 [Investigations](investigations/)
Real incidents from the lab, worked end to end with evidence attached.
*   **Currently:** [Wazuh SIEM recovery and CIS hardening](investigations/wazuh-siem-recovery-2026-04/) — a full log-ingestion outage diagnosed and fixed, with the hardening audit that followed.

### 📐 [Methodology](methodology.md) · [Roadmap](roadmap.md)
The incident-handling process these write-ups follow (NIST SP 800-61 r2), and what is being built next.

---
<div align="center">
  <i>Disclaimer: All activities documented in this portfolio are performed in controlled, legal environments for educational purposes.</i>
</div>
