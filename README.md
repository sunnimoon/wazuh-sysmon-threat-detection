# Wazuh Sysmon Threat Detection Lab

## Overview

This project demonstrates the detection and analysis of suspicious PowerShell activity using Sysmon and Wazuh SIEM.

A Windows 10 endpoint was configured with Sysmon to generate detailed process telemetry, which was forwarded to Wazuh for analysis. Detection rules were triggered based on PowerShell execution behavior, and the activity was investigated using command-line and process correlation.

This lab simulates real-world SOC workflows including log ingestion, alert detection, and incident investigation.

**Status:** Completed

---

## Tools & Technologies

- Wazuh (SIEM)
- Sysmon
- Windows 10 VM (endpoint agent)
- Ubuntu Desktop (Wazuh server & dashboard)
- Windows Event Viewer
- VirtualBox

---

## Lab Environment

- Sysmon installed and configured on Windows 10 endpoint
- Wazuh agent installed on Windows endpoint
- Sysmon logs forwarded from Windows to Wazuh
- Alerts reviewed and investigated in Wazuh dashboard

---

## Scenario

PowerShell activity was generated on the Windows endpoint to simulate suspicious behavior commonly investigated in SOC environments.

---

## Investigation Process

### 1. Endpoint Telemetry Configuration

- Installed and configured Sysmon on Windows endpoint
- Verified Sysmon process creation logs in Windows Event Viewer
- Confirmed Event ID 1 process creation events were generated

### 2. Agent Deployment

- Installed and configured Wazuh agent on Windows endpoint
- Connected Windows endpoint to Wazuh manager
- Verified successful connection between endpoint and SIEM

### 3. Log Ingestion

- Configured Wazuh agent to collect Sysmon Operational logs
- Forwarded Sysmon telemetry into Wazuh
- Verified Sysmon events were visible in Wazuh Threat Hunting

### 4. Alert Detection

- Wazuh detected PowerShell execution activity
- Alerts categorized as:
  - PowerShell process spawned PowerShell instance
  - Rule ID: 92027
  - MITRE Technique: T1059.001 PowerShell

### 5. Event Analysis

- Investigated alert details in Wazuh
- Identified key attributes:
  - Agent: WIN10-LAB
  - Process: powershell.exe
  - Command Line: powershell.exe -ExecutionPolicy Bypass
  - Parent Process: powershell.exe
  - User: DESKTOP-FFHSRE6\sunnimoon

### 6. Event Correlation

- Correlated Wazuh alerts with Sysmon endpoint logs
- Confirmed activity aligned with:
  - Event ID 1: Process Creation
  - Event ID 11: File Creation

PowerShell execution with ExecutionPolicy Bypass was generated manually on the Windows endpoint to simulate suspicious activity and validate detection capabilities.

---

## Findings

- PowerShell execution with ExecutionPolicy Bypass was detected
- The activity involved PowerShell spawning another PowerShell process
- Command-line analysis confirmed use of bypass flags commonly associated with malicious scripts
- Wazuh successfully mapped the activity to MITRE ATT&CK technique T1059.001
- File creation activity was observed in a temporary directory commonly used by malware

---

## Recommended Response & Mitigation

- Investigate PowerShell activity and validate whether execution was authorized
- Review command-line arguments for suspicious flags such as ExecutionPolicy Bypass
- Restrict unnecessary PowerShell usage where appropriate
- Enable PowerShell logging and script block logging in enterprise environments
- Monitor temporary directories for suspicious file creation activity

The PowerShell activity was generated intentionally on the Windows endpoint to simulate suspicious behavior and validate detection capabilities.

---

## Evidence

### Figure 1: Sysmon Process Creation Events

<img width="1026" height="768" alt="01-sysmon-process-events-overview png" src="https://github.com/user-attachments/assets/d850e4b1-b990-4080-aea5-98ee3f723813" />


### Figure 2: Process Creation Details

<img width="1024" height="769" alt="02-process-execution-details" src="https://github.com/user-attachments/assets/1bff569e-a253-498a-aa37-17fd53acab3f" />


### Figure 3: Sysmon PowerShell Execution Analysis

<img width="1025" height="768" alt="03-suspicious-powershell-execution" src="https://github.com/user-attachments/assets/51ba6526-6438-4894-a744-c0a6b416dc1f" />


### Figure 4: Wazuh Sysmon Events Overview

<img width="1274" height="800" alt="04-wazuh-sysmon-events-overview" src="https://github.com/user-attachments/assets/ce1940d5-53bd-4813-92d0-1b0f4cdf2dd1" />


### Figure 5: Wazuh PowerShell Command Line Analysis

<img width="1281" height="800" alt="05-wazuh-powershell-commandline-analysis png" src="https://github.com/user-attachments/assets/08405510-d797-4ca2-8956-6320184446c3" />


### Figure 6: Wazuh PowerShell Detection Alert

<img width="1277" height="797" alt="06-wazuh-powershell-detection-alert png" src="https://github.com/user-attachments/assets/96fd364f-e808-44c5-8e19-6478415ea122" />


### Figure 7: Wazuh Dashboard Overview

<img width="1278" height="799" alt="07-wazuh-dashboard-overview png" src="https://github.com/user-attachments/assets/8732acdf-635f-40f8-82b5-f574a0962bbe" />



---

## Skills Demonstrated

- SIEM monitoring and alert investigation
- Sysmon endpoint telemetry collection
- Windows process creation analysis
- Command-line analysis
- Log ingestion and event correlation
- MITRE ATT&CK mapping
- Basic threat detection and incident investigation
