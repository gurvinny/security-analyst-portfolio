# 🧪 Lab Writeup: Lookup (Easy)

<div align="center">
  <img src="https://img.shields.io/badge/Lab-TryHackMe-1F2937?style=for-the-badge&logo=tryhackme&logoColor=60A5FA" />
</div>

**Platform:** TryHackMe
**Date:** 2026-01-24
**Objective:** Simulate a realistic attack workflow demonstrating network & web enumeration, authentication bypass, command injection exploitation, and Linux privilege escalation to evaluate and improve SOC detection capabilities.

---

## 🔍 1. Executive Summary
The **Lookup** environment was successfully compromised through a multi-stage attack chain involving **virtual host enumeration, remote command execution, credential harvesting, and Linux privilege escalation**.

The compromise began with **subdomain discovery**, leading to an exposed **elFinder file manager** that enabled **Remote Code Execution (RCE)**. Post-exploitation enumeration revealed a vulnerable **SUID binary (`pwm`)**, which allowed credential extraction and lateral movement to the user **think**. Final escalation to **root** was achieved via a **sudo misconfiguration** involving the `look` binary.

This lab effectively demonstrates **full attack lifecycle execution**, emphasizing systematic reconnaissance, exploitation chaining, privilege escalation, and SOC detection opportunities.

## 🚨 2. Alert Triage (If Applicable)
*   **Alert Name:** Suspicious File Upload and RCE via elFinder
*   **Source IP:** Attacker IP (VPN)
*   **Destination IP:** `TARGET_MACHINE` (Lookup)
*   **Timestamp:** During initial access phase

## 🕵️ 3. Investigation & Analysis

### Initial Access
*   **How did the attacker get in?**
    An initial Nmap scan (`nmap -sC -sV -p- lookup.thm`) revealed exposed SSH (22) and HTTP (80) ports. Virtual host fuzzing using `ffuf` discovered the `files.lookup.thm` subdomain, which hosted an exposed **elFinder file manager**. The elFinder utility allowed image rotation and rename operations. By manipulating these functions, a PHP payload (`<?php system($_GET['cmd']); ?>`) was uploaded and executed, providing a `www-data` shell.
*   **Evidence:** Nmap scan results, `ffuf` discovery (`files.lookup.thm`), malicious PHP upload request captured (e.g., via Burp Suite), and a resulting `www-data` reverse shell.

### Execution & Persistence
*   **What commands were run?**
    The attacker stabilized the shell using a Python PTY spawn (`python3 -c 'import pty; pty.spawn("/bin/bash")'`). They then began system enumeration, searching for vulnerable SUID binaries (`find / -perm -4000 2>/dev/null`), leading to the discovery of `/usr/sbin/pwm`.
*   **Evidence:** Python process execution, execution of `find` commands, and interaction with the `/usr/sbin/pwm` binary.

### Privilege Escalation (If Applicable)
*   **How did the attacker gain SYSTEM/Root?**
    Lateral movement to the user `think` was achieved by exploiting a PATH hijacking vulnerability in the SUID binary `/usr/sbin/pwm`. The binary lacked absolute paths when executing the `id` command and reading `/home/<username>/.passwords`. The attacker created a malicious `id` script in `/tmp` and modified the PATH variable to point to it, enabling them to read the credentials.
    Vertical escalation to `root` was achieved by abusing a sudo misconfiguration (`sudo -l`), which permitted the user `think` to execute `/usr/bin/look` without a password. The `look` utility allowed arbitrary file reading, granting access to `/root/root.txt`.
*   **Evidence:** Modification of the `PATH` environment variable, execution of `/usr/sbin/pwm`, and execution of `sudo /usr/bin/look "" /root/root.txt`.

## 🛡️ 4. Indicators of Compromise (IOCs)

| Type | Indicator | Description |
| :--- | :--- | :--- |
| File Name | `*.php` | Malicious PHP payload uploaded via elFinder |
| Process | `nc`, `python3` | Reverse shell execution and PTY spawning |
| Command | `find / -perm -4000 2>/dev/null` | SUID binary enumeration |
| Path | `/tmp/id` | Malicious script created for PATH hijacking |
| Command | `sudo /usr/bin/look "" /root/root.txt` | Arbitrary file read via sudo misconfiguration |

## 💡 5. Detection Opportunities & Mitigation

### Detection
*   **Splunk Web Traffic Alert:** Create an alert in **Splunk** monitoring Apache/Nginx access logs for anomalous file uploads and subsequent execution, specifically targeting `.php` extensions in directories known for image uploads.
*   **Splunk Process Creation Alert:** Monitor **Windows/Linux** process creation events (e.g., Sysmon Event ID 1 or Auditd logs) for the execution of web server processes (like `www-data`) spawning interactive shells (`/bin/bash`, `nc`, or `python` PTY shells).
*   **Sigma Rule (PATH Hijacking):** Develop a **Sigma** rule to detect suspicious modifications to the `PATH` environment variable followed by the execution of known vulnerable SUID binaries (like `pwm` in this scenario).
*   **Sigma Rule (Sudo Misuse):** Create a **Sigma** rule triggering on `sudo` executions that leverage specific binaries (e.g., `look`, `less`, `more`) capable of arbitrary file reading when used with unrestricted arguments.

### Mitigation
*   **Authentication and Access Controls:** Enforce strict authentication on all internal administrative tools, including exposed services like elFinder.
*   **Input Validation:** Implement robust, server-side MIME type validation and file renaming to prevent malicious file uploads (e.g., disallowing `.php` extensions).
*   **Secure Coding Practices:** Audit custom SUID binaries to ensure they use absolute paths for system commands to prevent PATH hijacking vulnerabilities.
*   **Principle of Least Privilege:** Strictly audit and whitelist commands permitted via `sudo`. Remove file-reading utilities from unrestricted `sudo` configurations.
