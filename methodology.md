# SOC Analysis Methodology

## 1) Alert Triage
- Validate source and alert type
- Identify affected user/host/service
- Determine severity and scope
- Check for common false positives

## 2) Investigation
- Collect relevant logs (auth, web, endpoint, DNS)
- Extract Indicators of Compromise (IOCs)
- Build a timeline of events
- Look for lateral movement or persistence

## 3) Containment
- Isolate impacted hosts (if possible)
- Disable/rotate credentials and tokens
- Block malicious domains/IPs/hashes

## 4) Eradication & Recovery
- Remove malicious artifacts
- Patch root cause (vuln/misconfig)
- Restore services, monitor for recurrence

## 5) Lessons Learned
- Improve detections and alert logic
- Document playbook updates
- Create preventive hardening tasks
