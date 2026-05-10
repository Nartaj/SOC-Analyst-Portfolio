
# Technical Write-up: ElasticCase Lab Analysis

## Executive Summary
During the investigation in Elastic SIEM, I identified a multi-stage attack involving phishing-based initial access, malicious DLL execution, defense evasion, and cross-platform exploitation (Log4Shell & PwnKit). The attacker successfully established remote access and escalated privileges to root.

---

## Phase 1: Initial Access (Windows)
**Technique:** [T1204.002](https://attack.mitre.org/techniques/T1204/002/) — User Execution: Malicious File

The user `ahmed` executed a phishing payload disguised with a double extension to mimic a PDF document.

*   **Hostname:** DESKTOP-Q1SL9P2
*   **File Name:** `Acount_details.pdf.exe`
*   **Attacker IP:** `192.168.1.10`

**KQL Hunting Query:**
```kql
file.name : "Acount_details.pdf.exe" or process.name : "Acount_details.pdf.exe"
