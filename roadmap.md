<div align="center">

  <h1>🗺️ Career Roadmap — SOC Tier 1 Focus</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Career_Path-Security_Operations-1F2937?style=for-the-badge&logo=target&logoColor=60A5FA" alt="Status" />
  </p>
</div>

> **Last reviewed:** August 2026. Phases are dated rather than relative, so staleness is visible.

---

## 🎯 The Mission
The following structured roadmap details my professional progression to become a highly proficient, analytical Tier 1 Security Operations Center (SOC) Analyst. This strategic plan prioritizes practical execution, log aggregation mastery, and incident response methodology over theoretical understanding alone.

---

## 🟢 Phase 1: Foundations & Core Competencies (Complete)
*Establishing the critical baseline required to interpret enterprise infrastructure and identify architectural anomalies.*

### **Operating Systems & Infrastructure**
*   **Linux Fundamentals:** Advanced command-line operations (Bash), file permission auditing, service management (Systemd), identity administration, and `/var/log/` parsing.
*   **Windows Administration:** Core administrative concepts, Active Directory (AD) architecture, PowerShell fundamentals, Windows Event Log analysis (Security, System, Application), and baseline Sysmon configuration.
*   **Networking Concepts:** TCP/IP model deep dive, routing protocols (pfSense), layer 2 switching, DNS, DHCP, HTTP/S, and TCP/UDP port mapping.

### **Security Concepts & Attack Vectors**
*   **Web Attack Basics:** Comprehensive understanding of the OWASP Top 10 (Injection, Broken Access Control, Security Misconfigurations).
*   **Malware Families:** Identifying key signatures and delivery mechanisms for Ransomware, Trojans, Rootkits, and Exploit Kits.

### **Validation & Achievements**
*   🏆 **Completed:** TryHackMe Cyber Security 101 Path (`100%`)
*   🏆 **In Progress:** TryHackMe SOC Level 1 Path (`70%`)

---

## 🟡 Phase 2: Log Analysis & Detection Engineering (Current Focus — through early 2027)
*Transitioning focus from identifying operational systems to proactively detecting compromise indicators (IOCs).*

### **Log Aggregation & SIEM Mastery**
*   **Splunk:** Developing proficiency in SPL (Search Processing Language) to aggregate disparate log sources, aggressively filter noise (False Positives), and engineer foundational dashboards/alerts.
*   **Elastic Stack (ELK):** Gaining operational experience with Elasticsearch, Logstash, and Kibana for centralized telemetry aggregation and visualization.

### **Detection Engineering & Standardization**
*   **Sigma Framework:** Engineering vendor-agnostic detection signatures (`.yml`) to systematically translate adversary behavior into high-fidelity alerts across any SIEM environment.
*   **MITRE ATT&CK Framework:** Mapping detection rules, SIEM searches, and incident response playbooks to specific adversary Tactics, Techniques, and Procedures (TTPs).

### **Incident Response Methodology**
*   **Alert Triage Workflow:** Validating True Positives against False Positives, contextualizing asset enrichment, and actively scoping the incident's blast radius.
*   **Playbook Development:** Expanding `soc-playbooks/` beyond the three written so far (brute force, phishing, ransomware) to cover Insider Threat detection and Web Application Exploit triage.

---

## 🟠 Phase 3: Threat Hunting & Advanced Analysis (2027)
*Executing proactive, intelligence-driven hunts to identify latent threats bypassing automated security telemetry.*

### **Threat Hunting Methodologies**
*   **Hypothesis-Driven Hunting:** Formulating aggressive, intelligence-led hypotheses based on current Threat Intelligence (e.g., CISA advisories) and actively hunting for specific IOCs or anomalous behavioral patterns within the enterprise.
*   **Data-Driven Hunting:** Conducting large-scale dataset analysis to identify statistical deviations or baseline anomalies (e.g., highly unusual outbound network connections or abnormal process injection).

### **Advanced Enterprise Architecture**
*   **Active Directory Deep Dive:** Analyzing Kerberos authentication flows, auditing Group Policy Objects (GPOs), and identifying common AD exploitation techniques (Pass-the-Hash, Golden Ticket, Kerberoasting).
*   **Cloud Logging Basics:** Familiarization with aggregating and analyzing AWS CloudTrail logs, Azure Monitor, and auditing multi-cloud configuration postures.

### **Strategic Certification Goals**
*   ✅ **CompTIA Security+** — earned
*   ✅ **CompTIA CySA+** — earned
*   🎯 **Splunk Core Certified Power User** (Planned)
*   🎯 **Blue Team Level 1 (BTL1)** (Planned)
