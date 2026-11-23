# SOC Incident Investigation Report 001

## Failed Login Attempts – Windows 11

**Project:** SOC Home Lab – Security Monitoring & Incident Detection  
**Monitoring platform:** Wazuh 4.14.10  
**Endpoint:** Rosemary-Windows11  
**Date:** 22 November 2026  
**Investigation type:** Authentication failure monitoring

### 1. Objective

The objective of this investigation was to simulate failed login attempts on a Windows 11 endpoint and verify whether Windows Security logs were successfully collected and detected by Wazuh.

### 2. Test procedure

- Created a separate test account named SOC-TestUser.
- Enabled Windows Logon auditing for successful and failed attempts.
- Generated three intentional incorrect-password attempts.
- Checked the Windows Security event log.
- Searched for the events in Wazuh Discover.

### 3. Evidence collected

| Field | Observed value |
|---|---|
| Windows Event ID | 4625 |
| Wazuh Rule ID | 60122 |
| Wazuh Rule Level | 5 |
| Rule Description | Logon Failure - Unknown user or bad password |
| Account | SOC-testuser |
| Logon Type | 2 – Interactive |
| Failure Status | 0xC000006D |
| Failure Substatus | 0xC000006A |
| Source Address | 127.0.0.1 |
| Events detected | 3 |

### 4. Analysis

Windows generated Event ID 4625 for the unsuccessful login attempts. The failure substatus 0xC000006A indicates an incorrect password.

Wazuh successfully collected all three events from the Windows endpoint and identified them using rule ID 60122, with a severity level of 5.

The source address was 127.0.0.1, indicating that the authentication attempts originated locally rather than from a remote network address.

### 5. Conclusion

The test successfully demonstrated the collection and detection of failed Windows login attempts using Wazuh.

The Windows endpoint, Wazuh agent and Wazuh server integration worked as expected during this test.

These events were intentionally generated as part of an authorised home lab exercise. They do not represent a confirmed malicious intrusion.

### 6. Evidence screenshots

- 01-Failed-Login-Event-4625.png
- 02-Wazuh-Failed-Login-Detection.png

### 7. Outcome

**Status:** Successfully completed.

**Skills demonstrated:**
- Windows Security Event Log analysis
- Authentication failure monitoring
- Wazuh SIEM event investigation
- Basic security event triage
- Incident documentation
