<div align="center">

  <h1>💼 Resume Projects (Portfolio Extract)</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Projects-Portfolio-1F2937?style=for-the-badge&logo=github&logoColor=60A5FA" alt="Status" />
  </p>
</div>

---

## 🎯 The Mission
The following technical deployments and experiences are documented to demonstrate a comprehensive understanding of core Security Operations Center (SOC) competencies. The primary focus is **log aggregation, proactive threat detection, and structured incident response workflows.**

---

## 🛠️ Security Analyst Portfolio (GitHub)
*A structured knowledge base demonstrating SOC incident handling, detection engineering, and forensic analysis capabilities.*

*   **Incident Response Playbooks:** Established standard operating procedures (SOPs) for alert triage and containment, specifically addressing Phishing, Brute-Force, Malware Triage, and Web Application Attacks.
*   **Documentation & Reporting:** Authored comprehensive lab investigations (e.g., TryHackMe Walk-throughs) with a heavy emphasis on defensive intelligence, extracting actionable artifacts, and defining detection opportunities.
*   **Detection Engineering:** Authored and tuned custom **Sigma rules** and SIEM query strings (Splunk/Elastic), aligning threat behaviors to the **MITRE ATT&CK framework** to minimize false positives and elevate detection fidelity.

## 🔬 Practical Lab Investigations (TryHackMe)
*Continuous, hands-on training focused on parsing enterprise logs and replicating threat actor methodologies.*

*   **Progress Validation:** Completed **Cyber Security 101 Path (100%)** and actively advancing the **SOC Level 1 Path (70%)**.
*   **Methodology:** Executed structured enumeration, exploitation, and validation within sandboxed and legal environments to thoroughly understand the complete attack lifecycle.
*   **Defensive Focus:** Transformed offensive concepts into actionable defensive insights by rigorously analyzing SOC-relevant telemetry: Windows Event logs (Sysmon), endpoint process creation, and network protocol traffic (PCAP/Wireshark).
*   **Deliverables:** Synthesized professional incident write-ups designed for audit readiness, underscoring the *artifacts* left behind during post-exploitation rather than just the initial access exploit.

## 🏠 Enterprise Home Network Telemetry Lab ([GitHub](https://github.com/gurvinny/home-network-lab))
*A fully segmented, robustly monitored environment architected to simulate an enterprise network infrastructure for safe threat analysis.*

*   **Infrastructure Design:** Architected strict network segmentation utilizing **pfSense** and VLANs to isolate Lab, Guest, and IoT traffic, effectively minimizing the internal attack surface area.
*   **Intrusion Detection:** Engineered and deployed network-based Intrusion Detection/Prevention Systems (IDS/IPS), specifically **Snort/Suricata**, to automatically inspect and alert on anomalous traffic signatures.
*   **Centralized Logging:** Integrated **Splunk Universal Forwarders** across core infrastructure (Windows/Linux endpoints) to aggregate high-fidelity security events (authentication failures, suspicious process executions) into a centralized SIEM for dashboarding and proactive threat hunting.
*   **Objective:** Secured a persistent, monitored sandbox optimized for safe malware detonation, deep-packet inspection, and the empirical testing of new detection rules.

## 🎣 Automated Phish Extractor ([GitHub](https://github.com/gurvinny/Automated-Phish-Extractor))
*A Python-based automation tool engineered to streamline SOC workflows by automating the ingestion, parsing, and enrichment of malicious .eml files to combat alert fatigue.*

*   **IOC Automation:** Engineered a **Python** automation script to parse email headers (SPF, DKIM, DMARC), extract **Indicators of Compromise (IOCs)**, and calculate file hashes.
*   **Threat Enrichment:** Integrated external **Threat Intelligence** APIs (**VirusTotal v3**, **AbuseIPDB**) to automate malicious reputation checks and derive risk severity scores.
*   **Operational Security:** Developed automated defanging logic for extracted URLs, IPs, and domains to ensure safe sharing across teams and SOAR platforms without triggering enterprise perimeter alerts.
*   **Detection Engineering:** Authored actionable detection artifacts, including custom **YARA** and **Sigma rules**, derived from parsed telemetry to enable proactive **Threat Hunting** within **SIEM** environments.

## 🐬 Flipper Zero Hardware Security Lab ([GitHub](https://github.com/gurvinny/grv-flipper-lab))
*Exploration and documentation of physical security vulnerabilities, access controls, and radio frequency (RF) protocol manipulation.*

*   **Protocol Analysis:** Conducted rigorous hands-on research of physical access control systems, utilizing the Flipper Zero multi-tool for RFID/NFC payload cloning and Sub-GHz signal replay analysis.
*   **Vulnerability Assessment:** Demonstrated and documented practical attacks exploiting insecure wireless communications and legacy access controls.
*   **Mitigation Strategy:** Developed comprehensive mitigation strategies and defensive recommendations for RF-based vectors, actively translating physical security vulnerabilities into actionable IT security compliance policies.
