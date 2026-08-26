<div align="center">

  <h1>🔍 Detection Engineering & Threat Hunting</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" alt="Status" />
    <img src="https://img.shields.io/badge/Focus-Detection_Engineering-1F2937?style=for-the-badge&logo=shield&logoColor=60A5FA" alt="Focus" />
  </p>
</div>

---

## 🎯 The Mission
Detection logic written in vendor-agnostic **Sigma** and mapped to MITRE ATT&CK, so a rule can be translated to whichever SIEM is in front of it. The objective is low-noise alerts that survive contact with a real alert queue.

This directory is **early** — it currently holds one rule. It grows as lab investigations produce behaviour worth generalizing into a detection, rather than being filled with rules nobody has tested against real telemetry.

---

## 🏗️ Detection Methodology
To guarantee maximum visibility and minimize analyst fatigue, all detection artifacts authored within this repository rigorously adhere to the following principles:

-   **Behaviour over indicators:** target the *intent* behind an action (a download cradle, a shadow-copy deletion) rather than IPs and hashes, which rotate faster than a rule can be republished.
-   **False positives declared up front:** every rule names what will legitimately trip it. A rule that ships without that section moves the tuning cost onto whoever is on shift.
-   **Vendor Agnosticism:** Utilizing universally adopted formats, primarily **Sigma**, to ensure detection logic can be rapidly deployed and translated across disparate SIEM platforms (Splunk, Elastic, Sentinel).

---

## 📂 Active Intelligence & Telemetry Logic

### [📝 Suspicious PowerShell Download Cradle](sigma-rule-template.yml)
*   **Detects:** `powershell.exe` / `pwsh.exe` invoking `Net.WebClient` together with `DownloadString` — the classic in-memory fetch-and-execute pattern.
*   **ATT&CK:** T1059.001 (Command and Scripting Interpreter: PowerShell) · **Status:** experimental · **Level:** high
*   **Known false positives:** software-deployment and configuration-management tooling that legitimately fetches scripts at runtime.
*   Doubles as the house template — the metadata, log source and false-positive sections here are the shape every new rule follows.

---
<div align="center">
  <i>"Visibility is the foundation of defense. You cannot protect an environment against a threat you lack the telemetry to detect."</i>
</div>
