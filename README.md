# SOC-Home-Lab-Wazuh
A practical SOC home lab demonstrating security monitoring, endpoint detection and incident investigation using Wazuh, Sysmon and Windows 11.
# SOC Home Lab – Security Monitoring & Incident Detection

![Platform](https://img.shields.io/badge/Platform-Windows%2011-blue)
![SIEM](https://img.shields.io/badge/SIEM-Wazuh-orange)
![Endpoint Monitoring](https://img.shields.io/badge/Monitoring-Sysmon-green)
![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)

## Project Overview

This project demonstrates the design and implementation of a personal Security Operations Centre (SOC) home lab using Wazuh SIEM, Microsoft Sysmon, Windows 11 and VirtualBox.

The objective is to gain practical experience in endpoint security monitoring, security event collection, alert analysis and incident investigation.

The lab simulates common security monitoring scenarios and documents the investigation process through screenshots, technical observations and incident reports.

## Lab Environment

| Component | Technology |
|---|---|
| SIEM Platform | Wazuh 4.14.10 |
| Endpoint Operating System | Windows 11 |
| Endpoint Monitoring | Microsoft Sysmon 15.22 |
| Endpoint Agent | Wazuh Agent |
| Virtualization | Oracle VirtualBox |
| Command-line Tools | PowerShell |
| Log Sources | Windows Security Logs and Sysmon Operational Logs |

## Architecture

The lab uses the following event collection workflow:

```text
Windows 11 Endpoint
       |
       v
 Windows Security Logs
       |
       +-------------------+
       |                   |
       v                   v
  Sysmon Events       Security Events
       |                   |
       +---------+---------+
                 |
                 v
            Wazuh Agent
                 |
                 v
           Wazuh Manager
                 |
                 v
          Wazuh Dashboard
                 |
                 v
       Security Event Analysis
```

## Implemented Investigations

### 1. Failed Login Detection

**Windows Event ID:** 4625

- Generated controlled failed login attempts using a dedicated local test account.
- Enabled Windows logon failure auditing.
- Examined failed authentication events in Windows Security Logs.
- Identified the account name, logon type and authentication failure details.
- Verified the events in Wazuh Discover.

**Result:** Successfully detected and investigated three intentional failed login attempts.

### 2. PowerShell Process Monitoring

**Sysmon Event ID:** 1 – Process Create

- Configured Sysmon event collection through the Wazuh agent.
- Generated a harmless PowerShell test process.
- Investigated process creation events and command-line arguments.
- Identified the executable, process ID, user and parent process.
- Verified the command-line information in Wazuh Discover.

**Result:** Successfully verified PowerShell process telemetry from Windows through Sysmon and Wazuh.

### 3. Windows User Account Creation Detection

**Windows Event ID:** 4720

**Wazuh Rule ID:** 60109

- Checked Windows User Account Management auditing.
- Investigated a local test account creation event.
- Identified the account name and account creation details.
- Located the corresponding event in Wazuh Discover.
- Analysed the Wazuh rule description and severity level.

**Result:** Successfully detected a user account creation event with Wazuh Rule 60109 (Level 8).

## Tools and Technologies

- Wazuh SIEM
- Microsoft Sysmon
- Windows 11
- Windows Event Viewer
- Windows Security Logs
- PowerShell
- Oracle VirtualBox
- MITRE ATT&CK

## Repository Structure

```text
SOC-Home-Lab-Wazuh/
│
├── README.md
│
├── screenshots/
│   ├── 01-Environment-Setup/
│   ├── 02-Wazuh-Installation/
│   ├── 03-Windows-Agent/
│   ├── 04-Sysmon-Installation/
│   └── 05-Security-Events/
│
├── investigations/
│   ├── Incident-Report-001-Failed-Login.md
│   ├── Incident-Report-002-PowerShell-Process-Monitoring.md
│   └── Incident-Report-003-User-Account-Creation.md
│
├── configuration/
│
└── final-report/
```

## Learning Outcomes

Through this project, I am developing practical skills in:

- SIEM deployment and endpoint integration.
- Windows event log analysis.
- Endpoint telemetry collection using Sysmon.
- Authentication and account management monitoring.
- PowerShell process investigation.
- Security alert analysis and interpretation.
- Incident documentation and evidence collection.

## Project Status

**In Progress**

Further planned activities include:

- User privilege and group membership monitoring.
- Network connection monitoring.
- Additional Windows security event investigations.
- Custom Wazuh detection rules.
- Final technical documentation and investigation summary.

## Disclaimer

This is a personal cybersecurity learning project conducted in a controlled virtual lab environment. All simulated security activities were intentionally generated for educational and monitoring-validation purposes.
