# 🎣 Phishing Analysis Playbook

<div align="center">
  <img src="https://img.shields.io/badge/Playbook-Phishing-1F2937?style=for-the-badge&logo=minutemailer&logoColor=60A5FA" />
</div>

## 1. Preparation
*   Ensure access to email security gateways (e.g., Proofpoint, Mimecast) and SIEM.
*   Have sandbox environments (e.g., Any.Run, Joe Sandbox) ready for URL/Attachment analysis.

## 2. Detection & Alerting
*   **Trigger:** User reported email via Phish Alarm, or automated alert from email gateway.
*   **Initial Info Needed:** Sender Address, Recipient(s), Subject, Date/Time, Message ID.

## 3. Investigation
### 3.1. Header Analysis
*   Analyze `Received` headers to trace the email's origin path.
*   Verify SPF, DKIM, and DMARC results. Did the email fail authentication but still get delivered?
*   Check the `Reply-To` address against the `From` address.

### 3.2. Link/URL Analysis
*   Extract all URLs (use tools like `CyberChef` to defang: `hxxp://malicious[.]com`).
*   Check domain age, reputation (VirusTotal, URLhaus), and categorization.
*   *Do not click the link on a production machine.* Use a sandbox or urlscan.io.

### 3.3. Attachment Analysis
*   Extract file hashes (MD5, SHA256) and check reputation (VirusTotal).
*   If unknown, detonate in a secure sandbox to observe behavior (process creation, network connections).
*   Look for macros (VBA) in Office documents or hidden executables.

## 4. Containment
*   Purge the malicious email from all recipient inboxes (e.g., via O365 Compliance Search).
*   Block the malicious sender domain/IP on the email gateway.
*   Block any malicious URLs/IPs extracted during analysis on the web proxy/firewall.

## 5. Eradication & Recovery
*   If a user clicked the link or opened the attachment:
    *   Isolate the host immediately.
    *   Force a password reset for the compromised user.
    *   Initiate full endpoint antivirus/EDR scan.
*   Monitor for unauthorized access or lateral movement originating from the affected host.

## 6. Post-Incident Activity (Lessons Learned)
*   Update email gateway filtering rules.
*   Create SIEM alerts for the newly identified IOCs (domains, IPs, hashes).
*   Determine if additional user security awareness training is required.
