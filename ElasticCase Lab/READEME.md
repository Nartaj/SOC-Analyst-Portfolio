
# ElasticCase Digital Forensics & Incident Response (DFIR) Lab

«Detailed step-by-step solutions can be found in SOLUTION.md».

## Overview
This repository contains my technical walkthrough and analysis of the **ElasticCase** lab from CyberDefenders. The objective was to investigate a security breach on a Windows workstation using the Elastic Stack (ELK).

## Scenario
An alert was triggered indicating suspicious activity on a corporate endpoint. The goal was to analyze ingested logs (Winlogbeat, Sysmon, Powershell) to reconstruct the attacker's actions, identify the malware used, and determine the extent of the compromise.

## Tech Stack
*   **SIEM:** Elastic Search & Kibana
*   **Data Source:** Winlogbeat & Sysmon
*   **Query Language:** KQL (Kibana Query Language)

## Investigation Methodology
My approach focused on reconstructing the attack timeline by pivoting through indexed data. I utilized **KQL** to construct complex filters for deep-dive analysis, focusing on:

*   **Log Correlation:** Manually correlating Sysmon events (Event ID 1 for processes, ID 3 for network) to map the attacker's footprint.
*   **Query Optimization:** Leveraged AI-assisted KQL generation to accelerate the construction of specific filters, allowing for more time-efficient threat hunting and artifact discovery.
*   **Behavioral Analysis:** Identifying anomalies in command-line arguments and parent-child process trees to distinguish between legitimate system activity and malicious execution.

### 1. Initial Access & Execution
*   Analyzed process creation events to identify the entry point.
*   Focused on suspicious parent-child process relationships (e.g., `explorer.exe` spawning `powershell.exe`).
*   **Key Skill:** Filtering `event.code: 1` (Process Creation) to track execution flow.

### 2. Persistence & Lateral Movement
*   Investigated registry modifications and scheduled tasks designed to maintain access.
*   Used KQL to isolate encoded PowerShell commands often used for obfuscation.
*   *Example Query:* `process.args: *EncodedCommand*`

### 3. Indicator of Compromise (IoC) Identification
*   Extracted malicious IP addresses, domain names, and file hashes from the logs.
*   Correlated network connections (`event.code: 3`) with specific process IDs (PIDs) to identify C2 (Command & Control) communication.

## Key Findings
*   **Malicious Scripting:** Identified heavily obfuscated PowerShell scripts used for initial staging.
*   **Data Exfiltration:** Tracked unusual outbound traffic spikes indicating potential data theft.
*   **Artifact Recovery:** Successfully identified the specific malware family by analyzing file paths and naming conventions used by the threat actor.

## Conclusion
The lab demonstrated the power of the Elastic Stack in modern SOC operations. By leveraging **KQL**, I was able to pivot through massive datasets to find "the needle in the haystack" and build a timeline of the attack.
