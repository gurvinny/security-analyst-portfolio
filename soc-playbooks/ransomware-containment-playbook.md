# 🛑 Ransomware Containment & Eradication Playbook

<div align="center">
  <img src="https://img.shields.io/badge/Playbook-Ransomware-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" />
</div>

## 1. Preparation
*   Ensure access to SIEM (**Splunk**) for centralized log analysis of endpoint, identity, and network activity.
*   Verify access to endpoint detection and response (EDR) consoles for **Windows** environments.
*   Maintain updated network diagrams and access to network perimeter controls (e.g., **pfSense** firewalls).
*   Have specialized analysis tools like **Wireshark** (packet capture), **Burp Suite** (HTTP traffic interception), and **Python** (custom scripting) ready for deep investigation.

## 2. Detection & Alerting
*   **Trigger:** Automated alerts from EDR (e.g., mass file modifications, shadow copy deletion via `vssadmin`), sudden spikes in network traffic to unknown external IPs, or user reports of locked files and ransom notes.
*   **Initial Info Needed:** Affected Hostname/IP, Logged-in User, Timestamp of first suspicious activity, Alert Source (EDR, Splunk, User).

## 3. Investigation
### 3.1. Endpoint Analysis (Windows)
*   Query **Splunk** for Event IDs related to process creation (Event ID 4688) or file share access (Event ID 5140) to trace lateral movement.
*   Analyze the affected **Windows** host for malicious payloads, unexpected scheduled tasks, and persistence mechanisms.
*   Identify encrypted file extensions and search for the ransom note to identify the ransomware family.

### 3.2. Network Analysis
*   Use **Wireshark** to capture and analyze network traffic from the affected subnet. Look for beaconing behavior or data exfiltration prior to encryption.
*   If the ransomware communicates via HTTP/HTTPS, use **Burp Suite** (in a proxy/sandbox environment) to intercept and analyze the C2 check-in requests.
*   Review **pfSense** firewall logs for unusual outbound connections, especially over non-standard ports or known Tor entry nodes.

### 3.3. Payload Analysis
*   If a malicious executable or script is recovered, perform safe static analysis in an isolated sandbox.
*   Utilize custom **Python** scripts to safely parse, deobfuscate, and extract strings, URLs, or IP addresses from the dumped payload.

## 4. Containment
*   **Immediate Isolation:** Disconnect the compromised **Windows** endpoint from the network (physically or via EDR network isolation) to prevent lateral spread. *Do not power off the machine* to preserve volatile memory.
*   **Network Blocking:** Implement emergency block rules in **pfSense** to drop traffic to identified C2 IP addresses and domains.
*   Disable the compromised user's Active Directory account to stop further access to internal network file shares.

## 5. Eradication & Recovery
*   Wipe the infected endpoint completely and re-image with a known good, clean OS baseline.
*   Restore encrypted data from offline or immutable backups. Verify the integrity of the backup before restoration.
*   Force a global password reset for any user accounts that were active on the compromised machine.
*   Conduct a full EDR sweep across the environment using identified Indicators of Compromise (IOCs) to ensure no secondary backdoors remain.

## 6. Post-Incident Activity (Lessons Learned)
*   Develop and implement **Sigma** rules based on the adversary's techniques (e.g., detecting `vssadmin.exe Delete Shadows` or suspicious PowerShell execution) to improve future detection capabilities in Splunk.
*   Review and tighten lateral movement defenses, such as enforcing network segmentation and restricting local administrator privileges.
*   Conduct a post-incident review meeting with the team to identify gaps in response time or tool visibility.
