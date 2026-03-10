# 🛡️ Brute Force / Credential Stuffing Playbook

<div align="center">
  <img src="https://img.shields.io/badge/Playbook-Brute%20Force-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" />
</div>

## 1. Preparation
*   Ensure access to SIEM (**Splunk**) for centralized log analysis of authentication events across on-premise and cloud environments.
*   Verify access to Identity and Access Management (IAM) platforms (e.g., Active Directory, Azure AD, Okta).
*   Maintain updated geographic blocklists and have access to network perimeter controls (e.g., **pfSense** firewalls, WAFs).
*   Develop custom **Python** scripts for rapid analysis of large authentication log datasets (e.g., parsing user agents, ASN lookups).

## 2. Detection & Alerting
*   **Trigger:** High volume of failed login attempts, multiple accounts targeted from a single IP, a single account targeted from many IPs (password spraying), or a successful login following a string of failures.
*   **Initial Info Needed:** Targeted Username(s), Source IP Address(es), User-Agent(s), Timestamp of the activity, Affected Service (e.g., O365, VPN, SSH).

## 3. Investigation
### 3.1. Authentication Log Analysis
*   Query **Splunk** for Event IDs related to authentication failures (e.g., **Windows** Event ID 4625) and successful logons (Event ID 4624).
*   Analyze the timeframe, source IP addresses, and user agents involved. Determine if the attack is focused on a specific region or globally distributed.
*   Identify whether the activity represents a traditional brute force (one account, many passwords) or credential stuffing/password spraying (many accounts, few passwords).

### 3.2. Post-Login Activity Check
*   If a successful login is detected from a suspicious IP during the brute force window, immediately trace post-login actions.
*   Check for unauthorized access to internal resources, creation of inbox rules (e.g., O365 email forwarding), or unusual data access patterns.

## 4. Containment
*   **Immediate Account Action:** Temporarily lock or force a password reset for impacted user accounts to prevent unauthorized access.
*   **Network Blocking:** Implement emergency block rules in **pfSense** or the WAF to drop traffic from the identified abusive IP addresses or subnets.
*   Revoke any active sessions or authentication tokens associated with the compromised accounts.

## 5. Eradication & Recovery
*   Assist users in regaining access post-password reset, ensuring they use strong, unique passwords.
*   Enforce Multi-Factor Authentication (MFA) on all externally facing services.
*   If unauthorized access occurred, initiate an incident response to identify any potential data exfiltration or lateral movement.

## 6. Post-Incident Activity (Lessons Learned)
*   Update threshold-based alerts in **Splunk** (e.g., triggering after 10 failed attempts within 5 minutes from a single IP).
*   Implement or refine rate limiting and geographic restrictions (geo-blocking) on external login portals.
*   Develop **Sigma** rules to better detect distributed credential stuffing campaigns based on identified behavioral patterns.
