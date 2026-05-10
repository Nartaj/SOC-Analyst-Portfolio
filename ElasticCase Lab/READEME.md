# ElasticCase: Cross-Platform Incident Investigation

## Project Overview
This repository contains a deep-dive forensic analysis of the **ElasticCase** lab from CyberDefenders. The investigation covers a complex, multi-stage attack targeting both Windows and Linux environments, reconstructed using the **Elastic Stack (ELK)**.

## Key Objectives
*   Identify the initial access vector and malware execution flow.
*   Analyze defense evasion techniques and registry tampering.
*   Investigate Linux-based exploits including **Log4Shell (RCE)** and **PwnKit (LPE)**.
*   Develop robust **KQL queries** for threat hunting and incident reconstruction.

## Technical Stack
*   **SIEM:** Elastic Search & Kibana
*   **Log Sources:** Winlogbeat, Sysmon, Auditd, Application Logs (Solr)
*   **Methodology:** MITRE ATT&CK Framework Mapping
*   **Language:** KQL (Kibana Query Language)

## Analysis Summary
The attack lifecycle followed a classic Kill Chain:
1.  **Initial Access:** Phishing via double-extension executable.
2.  **Execution:** Proxy execution through `rundll32.exe`.
3.  **Persistence/Evasion:** Tampering with FIPS algorithm policies in the Windows Registry.
4.  **Lateral Movement:** Exploitation of CVE-2021-44228 (Log4Shell) on a Linux host.
5.  **Privilege Escalation:** Leveraging CVE-2021-4034 (PwnKit) to gain root access.

---

## Detailed Solution
Detailed step-by-step analysis, including KQL queries and Indicators of Compromise (IOCs), can be found in the full write-up:

[![View Solution](https://img.shields.io/badge/Write--up-View%20Technical%20Report-blue?style=for-the-badge&logo=elastic-stack)](./SOLUTION.md)

---
*Note: This investigation was performed in a controlled lab environment for educational purposes.*
