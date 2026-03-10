# 🎣 Phishing Response Playbook

<div align="center">
  <img src="https://img.shields.io/badge/Playbook-Phishing%20Response-1F2937?style=for-the-badge&logo=minutemailer&logoColor=60A5FA" />
</div>

## 1. Preparation
*   Ensure access to SIEM (**Splunk**) for centralized log analysis of authentication, proxy, and email gateway events.
*   Verify access to email security gateways (e.g., Proofpoint, Mimecast) and Office 365/Google Workspace admin consoles.
*   Maintain sandbox environments (e.g., Any.Run, Joe Sandbox) for secure URL and attachment analysis.
*   Have specialized analysis tools like **Wireshark** (packet capture) and **Burp Suite** (HTTP traffic interception) ready for deep investigation of malicious links.

## 2. Detection & Alerting
*   **Trigger:** User-reported email via Phish Alarm, or automated alert from the email gateway or SIEM.
*   **Initial Info Needed:** Reported email, sender address, recipient(s), subject, URLs/links, attachments, date/time, and message ID.

## 3. Investigation
### 3.1. Triage & Impact Assessment
*   Identify the reported email and extract the sender, subject, links, and attachments.
*   Determine if the user interacted with the email (e.g., clicked a link, entered credentials, or opened an attachment).

### 3.2. Technical Analysis
*   Review email headers to trace the origin and verify authentication (SPF, DKIM, DMARC).
*   Use **Python** scripts to automate the extraction of URLs and IOCs from the email body.
*   Analyze link destinations in a sandbox or using tools like `urlscan.io`. Use **Burp Suite** to inspect intermediate redirects and dropped payloads if necessary.
*   Query **Splunk** for authentication logs. Check for suspicious logins, impossible travel, new devices, or unusual MFA prompts associated with the user.

## 4. Containment
*   **Immediate Account Action:** Reset credentials and revoke active sessions/tokens for users who entered their credentials.
*   **Network Blocking:** Block the malicious sender, domain, or URL in the email gateway and DNS/proxy configurations.
*   Purge the malicious email from all recipient inboxes (e.g., via O365 Compliance Search).

## 5. Eradication & Recovery
*   Notify impacted users and stakeholders, providing guidance on identifying future phishing attempts.
*   Ensure the compromised user has regained secure access with strong, unique credentials and MFA enabled.
*   If an attachment was opened, initiate a full endpoint scan or isolate the host until a deeper forensic analysis can be performed.

## 6. Post-Incident Activity (Lessons Learned)
*   Update awareness training to reflect the specific tactics used in the phishing campaign.
*   Refine email filtering rules to prevent similar emails from reaching user inboxes.
*   Develop **Sigma** rules to alert on the newly identified behavioral patterns or IOCs associated with the campaign.
