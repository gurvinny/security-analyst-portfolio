# Brute Force / Credential Stuffing Response

## Detection Signals
- High volume failed logins
- Multiple accounts from one IP
- One account from many IPs
- Success after many failures

## Investigation
- Identify targeted accounts, timeframe, IPs, user agents
- Check for successful login and post-login activity

## Response
- Lock/reset impacted accounts
- Enforce MFA, rate limiting, geo restrictions
- Block abusive IPs and tune detections
