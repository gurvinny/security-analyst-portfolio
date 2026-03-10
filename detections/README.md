<div align="center">

  <h1>🔍 Detection Engineering & Threat Hunting</h1>

  <p align="center">
    <img src="https://img.shields.io/badge/Status-Active-1F2937?style=for-the-badge&logoColor=60A5FA&borderColor=60A5FA" alt="Status" />
    <img src="https://img.shields.io/badge/Focus-Detection_Engineering-1F2937?style=for-the-badge&logoColor=60A5FA&borderColor=60A5FA" alt="Focus" />
  </p>
</div>

---

## 🎯 Overview
This directory serves as a repository for custom detection rules, SIEM queries, and threat hunting logic developed to identify malicious activity and indicators of compromise (IOCs) within an enterprise environment. The goal is to build robust, high-fidelity alerts mapped to the MITRE ATT&CK framework.

---

## 🏗️ Detection Methodology
The detections in this repository are designed to be actionable and reduce alert fatigue. When developing a new rule, the focus is on:
- **Intent vs. Action:** Differentiating normal administrative behavior from malicious intent.
- **Tuning & False Positives:** Defining exclusions to limit noise.
- **Vendor Agnosticism:** Utilizing universal formats (like Sigma) whenever possible to ensure rules can be deployed across various SIEM platforms.

---

## 📂 Resources & Rules

### [📝 Sigma Rule Template](sigma-rule-template.yml)
A standardized template for creating new Sigma rules. This template ensures all necessary metadata (Title, Status, Description, Author, Date), log sources, detection logic, and false positive definitions are consistently documented for every new rule.

---
<div align="center">
  <i>"Visibility is the foundation of defense. You can't protect what you can't see."</i>
</div>
