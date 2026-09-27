<div align="center">

# Security Analyst Portfolio

<p align="center">📍 New York City Metro Area | Security Engineering &amp; Security Operations</p>

<p align="center">
  <a href="https://www.linkedin.com/in/gurvin-s-6a02b3278/"><img src="https://img.shields.io/badge/LinkedIn-Connect-1F2937?style=for-the-badge&logoColor=60A5FA" alt="LinkedIn" /></a>
  <a href="#-certifications--training"><img src="https://img.shields.io/badge/Security%2B_%26_CySA%2B-Certified-success?style=for-the-badge&logo=comptia&logoColor=white" alt="Certified" /></a>
  <img src="https://img.shields.io/badge/Status-Actively_Seeking_Roles-success?style=for-the-badge" alt="Status" />
</p>
</div>

> **Last reviewed:** September 2026.

---

## 🚀 The Mission
CompTIA **Security+** and **CySA+** certified, working across security engineering and security operations: building and hardening the infrastructure, then monitoring it. Recent work has been SIEM recovery and CIS/USG benchmark hardening on **Wazuh**/OpenSearch, default-deny network segmentation on **pfSense**, and detection logic in **Sigma** mapped to **MITRE ATT&CK**.

Everything here was built and broken in a self-hosted lab, then documented the way a shift handover would need it: evidence attached, decisions justified, and the accepted risks named rather than omitted. Where a section is thin, it says so.

---

## 🔬 Featured Work

Ordered by strength of evidence; the first entry is backed by a tool-generated audit screenshot.

| Project | What it demonstrates | Stack | Link |
| :--- | :--- | :--- | :--- |
| **Wazuh SIEM Recovery & Hardening** | Diagnosed a total log-ingestion failure across the OpenSearch authentication chain and restored live alerting, then hardened the host to **88.9%** on the CIS Ubuntu 24.04 benchmark and **90.98%** on the USG Level 2 audit (435 of 471 rules passed; 36 remain open, 2 of them high severity). Scan evidence attached. | Wazuh · OpenSearch · Ubuntu | [Case study](investigations/wazuh-siem-recovery-2026-04/) |
| **Home Network Lab** | Default-deny, VLAN-segmented network on a dedicated edge appliance, with a named noise-suppression ruleset (`SOC_SILENCE_*`) and a full firewall log-analysis report mapped to MITRE ATT&CK. | pfSense · Wazuh | [Repo](https://github.com/gurvinny/home-network-lab) |
| **SPECTRE** | Wireless IDS built from dual ESP32-C5 sniffers: 802.11 frame ingestion, four detection rules, and threat forwarding to Wazuh as RFC 5424 syslog. Two rules are ATT&CK-mapped (**T1557** evil twin, **T1499** deauth flood); the flood and anomaly rules are not yet mapped. | ESP32-C5 · Python · Next.js | [Repo](https://github.com/gurvinny/spectre) |
| **Automated Phish Extractor** | Automates the repetitive first pass of phishing triage: IOC extraction and defanging, VirusTotal and AbuseIPDB enrichment, risk scoring, and a standardized IR report. CI across Python 3.10–3.13. | Python | [Repo](https://github.com/gurvinny/Automated-Phish-Extractor) |

---

## ⚙️ Technical Competencies

> Tools carrying a linked artifact in this repo or in the featured work above: Wazuh, pfSense,
> Sigma, MITRE ATT&CK, Python, Linux. The rest are working knowledge from labs and coursework,
> listed as such rather than as demonstrated deliverables.

| **Category** | **Technologies & Platforms** |
| :--- | :--- |
| **SIEM & Security Monitoring** | ![Wazuh](https://img.shields.io/badge/Wazuh-1F2937?style=flat-square&logo=elasticsearch&logoColor=60A5FA) &nbsp;·&nbsp; *learning:* ![Splunk](https://img.shields.io/badge/Splunk-374151?style=flat-square&logo=splunk&logoColor=9CA3AF) ![Elastic](https://img.shields.io/badge/Elastic-374151?style=flat-square&logo=elasticsearch&logoColor=9CA3AF) |
| **Network Traffic Analysis & Perimeter** | ![Wireshark](https://img.shields.io/badge/Wireshark-1F2937?style=flat-square&logo=wireshark&logoColor=60A5FA) ![pfSense](https://img.shields.io/badge/pfSense-1F2937?style=flat-square&logo=pfsense&logoColor=60A5FA) ![VLAN](https://img.shields.io/badge/VLAN_Segmentation-1F2937?style=flat-square&logoColor=60A5FA) |
| **Detection Engineering & Frameworks** | ![Sigma](https://img.shields.io/badge/Sigma-1F2937?style=flat-square&logoColor=60A5FA) ![MITRE ATT&CK](https://img.shields.io/badge/MITRE_ATT&CK-1F2937?style=flat-square&logoColor=60A5FA) |
| **Endpoint Security** | Host monitoring: Wazuh agents (FIM, auditd, SCA) |
| **Security Orchestration & Scripting** | ![Python](https://img.shields.io/badge/Python-1F2937?style=flat-square&logo=python&logoColor=60A5FA) ![Bash](https://img.shields.io/badge/Bash-1F2937?style=flat-square&logo=gnu-bash&logoColor=60A5FA) ![PowerShell](https://img.shields.io/badge/PowerShell-1F2937?style=flat-square&logoColor=60A5FA) |
| **Operating Systems** | ![Windows](https://img.shields.io/badge/Windows-1F2937?style=flat-square&logoColor=60A5FA) ![Linux](https://img.shields.io/badge/Linux-1F2937?style=flat-square&logo=linux&logoColor=60A5FA) |

<sub>Full-colour entries are deployed and operated in the home lab. Greyed *learning*
entries are in progress; see the <a href="roadmap.md">roadmap</a> for where each one stands.</sub>

---

## 📜 Certifications & Training

**B.S. Cybersecurity & Information Assurance** · Western Governors University · expected 02/2027

*   [![CompTIA CySA+](https://img.shields.io/badge/CompTIA-CySA%2B-1F2937?style=flat-square&logo=comptia&logoColor=60A5FA)](https://www.credly.com/earner/earned/badge/8ff86bbc-133d-46b6-b91e-7475ded8ed63) `Certified`
*   [![CompTIA Security+](https://img.shields.io/badge/CompTIA-Security%2B-1F2937?style=flat-square&logo=comptia&logoColor=60A5FA)](https://www.credly.com/earner/earned/badge/3714ff8f-276c-47f4-ac49-b1551eefefcc) `Certified`
*   [![CompTIA Network+](https://img.shields.io/badge/CompTIA-Network%2B-1F2937?style=flat-square&logo=comptia&logoColor=60A5FA)](https://www.credly.com/earner/earned/badge/7d61a205-31d0-4a51-bd04-3e227f634e3c) `Certified`
*   [![CompTIA A+](https://img.shields.io/badge/CompTIA-A%2B-1F2937?style=flat-square&logo=comptia&logoColor=60A5FA)](https://www.credly.com/earner/earned/badge/e33d46ab-136c-4ed0-a7e2-ad82078659ab) `Certified`

---

## 🛠️ Analytical Methodology

*   **Framework Alignment:** Mapping lab detections to **MITRE ATT&CK**. Tactics currently covered: Execution (T1059.001), Credential Access and Collection (T1557), and Impact (T1499).
*   **Incident Lifecycle:** Following the **NIST SP 800-61** lifecycle.
*   **Documentation:** A standardized write-up template: timeline, evidence, root cause, remediation.

---

## 📂 Portfolio Modules

### 📘 [Incident Response Playbooks](soc-playbooks/)
Structured standard operating procedures (SOPs) for triage, containment, and eradication.
*   **Analyst Focus:** Phishing Analysis, Ransomware Containment, Brute Force Triage.

### 🔍 [Detection Engineering](detections/)
Vendor-agnostic detection logic written in Sigma and mapped to ATT&CK.
*   **Currently:** one Sigma rule (PowerShell download cradle, T1059.001). This section is early; it grows as lab investigations produce detections worth generalizing.

### 🧪 [CTF Write-ups](labs/)
Forensic write-ups reconstructing attacker kill chains and the artifacts each stage leaves behind.
*   **Currently:** one full report (TryHackMe *Lookup*: elFinder RCE → SUID PATH hijack → root), plus the standard write-up template every report follows.

### 🔬 [Investigations](investigations/)
Real incidents from the lab, worked end to end with evidence attached.
*   **Currently:** [Wazuh SIEM recovery and CIS hardening](investigations/wazuh-siem-recovery-2026-04/): a full log-ingestion outage diagnosed and fixed, with the hardening audit that followed.

### 📐 [Methodology](methodology.md) · [Roadmap](roadmap.md)
The incident-handling process these write-ups follow (NIST SP 800-61), and what is being built next.

---

## Contributions

This repository is published as a record of completed work, not as a collaborative project.
Issues are disabled and pull requests are not reviewed or merged. Corrections, broken links and
security concerns are welcome; see the [security policy](https://github.com/gurvinny/.github/blob/main/SECURITY.md) for how to report them.

---

<div align="center">
  <i>Disclaimer: All activities documented in this portfolio are performed in controlled, legal environments for educational purposes.</i>
</div>
