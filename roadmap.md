# 🗺️ Career Roadmap — SOC Tier 1 Focus

<div align="center">
  <img src="https://img.shields.io/badge/Career_Path-Security_Operations-1F2937?style=for-the-badge&logo=target&logoColor=60A5FA" />
</div>

The following roadmap outlines my structured learning path to become a highly proficient Tier 1 Security Operations Center (SOC) Analyst. This plan prioritizes hands-on practical skills aligned with current industry demands.

---

## 🟢 Phase 1: Foundations & Core Competencies (Current Focus)
*Building the essential baseline knowledge required to understand how systems operate and communicate.*

### **Operating Systems & Infrastructure**
*   **Linux Fundamentals:** Command-line proficiency (Bash), file permissions, service management (Systemd), user administration, and system logging (`/var/log/`).
*   **Windows Administration:** Core concepts, Active Directory architecture, PowerShell basics, Windows Event Logs (Security, System, Application), and Sysmon configuration.
*   **Networking Concepts:** TCP/IP model, routing (pfSense), switching, DNS, DHCP, HTTP/S, and understanding standard ports/protocols.

### **Security Concepts & Attack Vectors**
*   **Web Attack Basics:** Understanding OWASP Top 10 (Injection, Authentication Failures, Cross-Site Scripting).
*   **Malware Families:** Familiarity with Ransomware, Trojans, Rootkits, and common delivery mechanisms (Phishing, Exploit Kits).

### **Achievements**
*   🏆 **Completed:** TryHackMe Cyber Security 101 Path (`100%`)
*   🏆 **In Progress:** TryHackMe SOC Level 1 Path (`70%`)

---

## 🟡 Phase 2: Log Analysis & Detection Engineering (Next 3-6 Months)
*Transitioning from understanding how systems work to identifying when they are compromised.*

### **Log Aggregation & SIEM Mastery**
*   **Splunk:** Mastering SPL (Search Processing Language) for aggregating logs, filtering noise, and building foundational dashboards/alerts.
*   **Elastic Stack (ELK):** Gaining hands-on experience with Elasticsearch, Logstash, and Kibana for centralized logging and visualization.

### **Detection Engineering & Standardization**
*   **Sigma Framework:** Writing vendor-agnostic detection rules (`.yml`) that translate adversary behavior into actionable alerts for any SIEM.
*   **MITRE ATT&CK Framework:** Mapping detection rules and incident response playbooks directly to specific Tactics, Techniques, and Procedures (TTPs).

### **Incident Response Methodology**
*   **Alert Triage Workflow:** Validating True/False Positives, contextualizing entities, and scoping the incident.
*   **Playbook Development:** Expanding the `soc-playbooks/` repository with detailed Standard Operating Procedures (SOPs) for Ransomware, Insider Threats, and Web Exploits.

---

## 🟠 Phase 3: Threat Hunting & Advanced Analysis (6-12 Months)
*Proactively searching for hidden threats that bypass automated security controls.*

### **Threat Hunting Methodologies**
*   **Hypothesis-Driven Hunting:** Formulating hypotheses based on recent Threat Intelligence (e.g., CISA advisories) and hunting for specific IOCs or anomalous behaviors within the environment.
*   **Data-Driven Hunting:** Analyzing large datasets to identify statistical outliers or deviations from baseline activity (e.g., unusual outbound network connections).

### **Advanced Enterprise Architecture**
*   **Active Directory Deep Dive:** Understanding Kerberos authentication, Group Policy Objects (GPOs), and common AD attacks (Pass-the-Hash, Golden Ticket, Kerberoasting).
*   **Cloud Logging Basics:** Familiarization with AWS CloudTrail, Azure Monitor, and identifying misconfigurations in cloud environments.

### **Certifications Goals**
*   🎯 **CompTIA Security+** (In Progress)
*   🎯 **Splunk Core Certified Power User** (Planned)
*   🎯 **Blue Team Level 1 (BTL1)** or **CompTIA CySA+** (Planned)
