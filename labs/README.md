<div align="center">

  <h1>🔬 Lab Investigations & Walkthroughs</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" alt="Status" />
    <img src="https://img.shields.io/badge/Focus-Blue_Team-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" alt="Focus" />
  </p>
</div>

---

## 🎯 The Mission
This directory contains comprehensive, professional-grade writeups of attack simulations, CTF challenges, and hands-on lab investigations. The focus is strictly on **defensive security operations**—analyzing artifacts left behind during post-exploitation, understanding adversary methodologies, and engineering high-fidelity detection strategies.

---

## 🏗️ Writeup Methodology
To maintain an aggressive, analytical standard consistent with modern SOC operations, **all lab writeups in this repository adhere strictly to a unified structural methodology:**

1. **Hero Section:** Dynamic status badges (Severity, Status, Primary Tool, Platform) for immediate contextual awareness.
2. **The Mission:** A concise, one-sentence objective defining the core focus of the investigation.
3. **Attack Topology:** A visual Mermaid.js flowchart mapping out the complete attack kill chain and actor progression.
4. **Executive Summary:** A high-level table summarizing critical phases of the compromise.
5. **Incident Timeline:** A structured sequence of events for chronological reconstruction.
6. **The Investigation:** Step-by-step forensic analysis, utilizing `<details>` and `<summary>` tags to encapsulate raw logs, PCAP analysis, and command-line execution artifacts.
7. **MITRE ATT&CK Mapping:** A clean Markdown table directly correlating the observed adversary behaviors against specific tactics and techniques.
8. **Closing (Remediation & Lessons Learned):** Actionable, defensive recommendations for mitigating the exploited vulnerabilities and engineering SIEM alerts to detect similar future activity.

---

## 📂 Active Investigations

### [TryHackMe Deployments](tryhackme/)
Walkthroughs focusing heavily on log aggregation, endpoint forensics (Sysmon), and network traffic analysis.
*   **[Lookup](tryhackme/easy/lookup/report.md)** (Easy) - Investigating anomalous web uploads (elFinder RCE), PATH hijacking, and SUID exploitation to develop actionable detection logic.

### [HackTheBox Deployments](hackthebox/)
*(Coming Soon)* - Advanced defensive scenarios and Sherlocks centered on enterprise incident response, lateral movement detection, and active threat hunting.

---
<div align="center">
  <i>"In security operations, knowing how the exploit functions is only the baseline. Engineering the telemetry to detect and contain it is the objective."</i>
</div>
