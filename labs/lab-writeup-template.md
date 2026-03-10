# 🧪 Lab Writeup: [Challenge/Lab Name]

<div align="center">
  <img src="https://img.shields.io/badge/Lab-TryHackMe-1F2937?style=for-the-badge&logo=tryhackme&logoColor=60A5FA" />
</div>

**Platform:** TryHackMe / Hack The Box / Custom
**Date:** YYYY-MM-DD
**Objective:** [Briefly describe the goal of the lab/challenge]

---

## 🔍 1. Executive Summary
Provide a high-level overview of the attack simulated in the lab. What was the initial vector, how did the attacker establish persistence, and what was the final objective (e.g., privilege escalation, data exfiltration)?

## 🚨 2. Alert Triage (If Applicable)
*   **Alert Name:**
*   **Source IP:**
*   **Destination IP:**
*   **Timestamp:**

## 🕵️ 3. Investigation & Analysis
Detail the steps taken to investigate the incident. Focus on the *logs* and *artifacts* found.

### Initial Access
*   How did the attacker get in? (e.g., Exploit against an unpatched web service, phishing).
*   **Evidence:** [Insert log snippet, screenshot of web traffic, or PCAP analysis].

### Execution & Persistence
*   What commands were run? Did they drop any payloads?
*   **Evidence:** [Insert Sysmon process creation logs, scheduled task creation logs].

### Privilege Escalation (If Applicable)
*   How did the attacker gain SYSTEM/Root?
*   **Evidence:** [Insert relevant logs or command history].

## 🛡️ 4. Indicators of Compromise (IOCs)
List the actionable items extracted during the investigation.

| Type | Indicator | Description |
| :--- | :--- | :--- |
| IP Address | `192.168.1.100` | Attacker C2 Server |
| File Hash (SHA256) | `e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855` | Malicious Payload |
| Domain | `malicious-domain[.]com` | Phishing Link |

## 💡 5. Detection Opportunities & Mitigation
Based on this lab, how could a SOC detect or prevent this attack in the future?

*   **Detection:** Create a Splunk alert looking for `[Specific Event ID]` combined with `[Specific Command Line Parameter]`. (Link to Sigma rule if created).
*   **Mitigation:** Ensure all external-facing web applications are patched. Implement Network Segmentation to prevent lateral movement.
