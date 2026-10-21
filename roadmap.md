<div align="center">

  <h1>🗺️ Career Roadmap: Security Operations</h1>
</div>

> **Last reviewed:** September 2026. Delivered work is dated by when it was performed, not when
> it was published here, and every row links to an artifact. Anything without an artifact is
> listed as in progress or planned, never as a capability.

---

## 🎯 The Mission

Three tracks run in parallel rather than in sequence: what I **detect and respond to**, what I
**build and secure**, and what I **study**. They feed each other. The lab produces the incidents,
the incidents produce the detections, and the coursework supplies the theory the other two lean on.

---

## 🔵 Track 1: Detection & Response

*Finding things in telemetry, then working them end to end.*

### Delivered

| Date | Work | Evidence |
| :--- | :--- | :--- |
| 2026-04 | Full log-ingestion outage diagnosed across the OpenSearch auth chain and restored, then host hardened to **88.9%** CIS Ubuntu 24.04 L1 and **90.98%** USG Level 2 (435 of 471 rules passed; 36 open, 2 high severity) | [Case study](investigations/wazuh-siem-recovery-2026-04/) |
| 2026-07 | Four wireless detection rules (deauth flood, evil twin, beacon/probe flood, RSSI anomaly) forwarding to Wazuh as RFC 5424. Two are ATT&CK-mapped: **T1557** (evil twin) and **T1499** (deauth flood); the flood and anomaly rules are not yet mapped | [SPECTRE](https://github.com/gurvinny/spectre) |
| 2026-04 | Firewall log-analysis report with a named noise-suppression ruleset, mapped to ATT&CK | [home-network-lab](https://github.com/gurvinny/home-network-lab) |
| 2026-04 | One vendor-agnostic Sigma rule, PowerShell download cradle (T1059.001) | [detections/](detections/) |
| 2026-03 | Three incident response playbooks: brute force, phishing, ransomware containment | [soc-playbooks/](soc-playbooks/) |
| 2026-01 | Full kill-chain reconstruction of the **TryHackMe _Lookup_** room (elFinder RCE to SUID PATH hijack to root), plus the write-up template every report follows | [labs/](labs/) |

### In progress

*   **TryHackMe SOC Level 1 Path.** Not yet complete, so it is not claimed as a credential elsewhere.
*   **Splunk.** Target: SPL searches, multi-source correlation, false-positive tuning, dashboards and alerts. No artifact yet.
*   **Elastic Stack.** Target: Elasticsearch, Logstash and Kibana for centralized telemetry. No artifact yet.

### Next

| Target | Goal |
| :--- | :--- |
| Q4 2026 | Grow `detections/` to five or more rules. It is the thinnest part of this portfolio and the roadmap says so. |
| Q1 2027 | Splunk lab with a published artifact, then the Splunk Core Certified Power User exam. |
| Q1 2027 | Active Directory detection lab: Kerberos flows, GPO auditing, and detection for Pass-the-Hash, Golden Ticket and Kerberoasting. |

### Later

*   Expand playbooks to insider threat and web application exploit triage.
*   **Threat hunting:** hypothesis-driven hunts against current advisories, and data-driven hunts for statistical deviation (unusual egress, abnormal process injection).
*   **Cloud telemetry:** AWS CloudTrail and Azure Monitor aggregation and analysis.
*   Restructure `methodology.md` around **NIST SP 800-61r3 / CSF 2.0**, which replaces the four-phase lifecycle with the six CSF Functions.

---

## 🟣 Track 2: Security Engineering

*Building the systems, then securing what I built. Most of the telemetry in Track 1 exists because of work in this one.*

### Delivered

| Date | Work | Evidence |
| :--- | :--- | :--- |
| 2026-07 | Wireless IDS built end to end: custom ESP32-C5 promiscuous firmware, UART ingest, standard-library detection engine, Next.js console, RFC 5424 forwarding to Wazuh | [SPECTRE](https://github.com/gurvinny/spectre) |
| 2026-09 | Supply-chain remediation: ten advisories closed including two critical unauthenticated RCEs (`GHSA-2xp9-vwfh-vxw4`, `CVE-2026-75604`), forced patched versions of 4 transitive deps via npm overrides, and removed the vulnerable image-optimizer route from the attack surface | [PR #20](https://github.com/gurvinny/spectre/pull/20) |
| 2026-09 | Exposure assessment treated as a step distinct from patching: each advisory triaged against the actual deployment, so the windows-hosted RCE was recorded as not applicable to Linux containers and patched anyway rather than counted as a hit | [PR #20](https://github.com/gurvinny/spectre/pull/20) |
| 2026-09 | Static analysis and dependency automation wired from nothing: CodeQL across JavaScript/TypeScript, Python and Actions, plus Dependabot across five ecosystems | [SPECTRE](https://github.com/gurvinny/spectre) |
| 2026-04 | Default-deny, VLAN-segmented network on a dedicated edge appliance, with forced DNS and NTP redirection on untrusted segments | [home-network-lab](https://github.com/gurvinny/home-network-lab) |
| 2026-03 | Phishing triage automation with IOC extraction and defanging, VirusTotal and AbuseIPDB enrichment, risk scoring and a standardized IR report. CI across Python 3.10 to 3.13 | [Automated Phish Extractor](https://github.com/gurvinny/Automated-Phish-Extractor) |

### Next

| Target | Goal |
| :--- | :--- |
| Q4 2026 | Publish the hardening process itself, not only the resulting scores, so the CIS and USG work is reproducible by a reader. |
| Q1 2027 | Detection-as-code: version and test detection logic the same way application code is tested. |

---

## 🟢 Track 3: Academic

*Formal coursework, running alongside both tracks above.*

Working through a **B.S. in Cybersecurity & Information Assurance** at Western Governors
University, expected **February 2027**. The degree is built around industry-standard
certifications rather than coursework alone, so each term produces a credential that stands on
its own outside the transcript.

Six are earned and listed with verification links in [Credentials](#-credentials) below.
**Remaining in the degree plan:** CompTIA Data+, CompTIA PenTest+ and ISC2 SSCP.

The lab work in the two tracks above is usually where the coursework gets applied first.

---

## 📜 Credentials

*   🎓 **B.S. Cybersecurity & Information Assurance**, Western Governors University · expected February 2027
*   ✅ [**CompTIA CySA+**](https://www.credly.com/badges/8ff86bbc-133d-46b6-b91e-7475ded8ed63) · earned June 2026
*   ✅ [**CompTIA Security+**](https://www.credly.com/badges/3714ff8f-276c-47f4-ac49-b1551eefefcc) · earned June 2026
*   ✅ [**CompTIA Network+**](https://www.credly.com/badges/7d61a205-31d0-4a51-bd04-3e227f634e3c) · earned September 2026
*   ✅ [**CompTIA A+**](https://www.credly.com/badges/e33d46ab-136c-4ed0-a7e2-ad82078659ab) · earned September 2026
*   ✅ [**LPI Linux Essentials**](https://www.credly.com/badges/0ac6a07e-05a6-4173-b617-e19b6308b1e5) · earned October 2026
*   ✅ [**ITIL 4 Foundation**](https://www.peoplecert.org/public-profile?ed=XCHu3ZqUTNIe%2fnJchle6lbije6RLjHX4) · earned October 2026
*   🏆 [**TryHackMe Cyber Security 101 Path**](https://tryhackme-certificates.s3-eu-west-1.amazonaws.com/THM-BPY9Y4IOOB.pdf) · completed February 2026
*   🎯 **Splunk Core Certified Power User** (planned, Q1 2027)
*   🎯 **Blue Team Level 1 (BTL1)** (later, no target date set)

---

## 🧱 Foundations (covered by A+, Network+, Security+ and CySA+)

*Exam-verified knowledge underlying everything above, listed for completeness rather than as achievements.*

Linux command line and service management, `/var/log/` parsing, Windows administration and Event
Log analysis, TCP/IP and layer 2 switching, DNS, DHCP and HTTP/S, common web application
vulnerabilities (injection, broken access control, security misconfiguration), and malware
families and delivery mechanisms.
