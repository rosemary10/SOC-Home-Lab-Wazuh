# Incident Report 002: PowerShell Process Monitoring

**Project:** SOC Home Lab – Security Monitoring & Incident Detection  
**Date:** 22 November 2026  
**Platform:** Windows 11  
**SIEM:** Wazuh 4.14.10  
**Endpoint Agent:** Rosemary-Windows11  
**Data Source:** Microsoft Sysmon – Operational Log

## 1. Objective

To verify that PowerShell process-creation events are captured by Sysmon, forwarded by the Wazuh agent, and searchable in the Wazuh dashboard.

## 2. Test Procedure

1. Opened Windows PowerShell.
2. Executed a harmless test command that launched a separate PowerShell process:

   ```powershell
   Start-Process powershell.exe -ArgumentList '-NoProfile -Command "Write-Output SOC_LAB_TEST"'
   ```

3. Checked the local Sysmon Operational event log for Event ID 1.
4. Identified the test process using its Process ID.
5. Searched for the process in Wazuh Discover.
6. Expanded the Wazuh event to inspect the recorded command line.

## 3. Evidence and Observations

### Sysmon findings

- Event ID: 1 – Process Create
- Process ID: 13396
- Process: powershell.exe
- User: LAPTOP-FUSDRPR6\LOQ
- Integrity Level: High
- MITRE technique label: T1059.001 – PowerShell
- Command: `Write-Output SOC_LAB_TEST`

Three matching local Sysmon records were returned for the test command.

### Wazuh findings

The event was successfully located in Wazuh Discover using the endpoint agent name and process ID.

- Agent name: Rosemary-Windows11
- Agent ID: 001
- Process ID: 13396
- Event source: Microsoft Sysmon
- Command-line field: `data.win.eventdata.commandLine`

The expanded Wazuh event displayed the complete PowerShell command, including the unique test string `SOC_LAB_TEST`.

Two matching Wazuh records were returned by the Process ID search.

## 4. Analysis

The experiment demonstrates that Sysmon can record PowerShell process-creation activity and that Wazuh can receive, index, and display the corresponding event.

The command-line field provides useful investigation context because it shows the executable and arguments used to start the process.

The MITRE ATT&CK label T1059.001 identifies PowerShell as the technique category. Its presence alone does not indicate malicious activity.

The test was intentionally generated for monitoring validation and did not represent an actual security incident.

## 5. Conclusion

The PowerShell process-monitoring test was successful.

The complete collection path was verified:

**Windows PowerShell → Sysmon → Wazuh Agent → Wazuh Discover**

The experiment confirms that process-creation telemetry and command-line information are available for endpoint investigation.
