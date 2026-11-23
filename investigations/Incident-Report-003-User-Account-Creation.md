# Incident Report 003: Windows User Account Creation Detection

**Project:** SOC Home Lab – Security Monitoring & Incident Detection  
**Date:** 22 November 2026  
**Platform:** Windows 11  
**SIEM:** Wazuh 4.14.10  
**Endpoint Agent:** Rosemary-Windows11  
**Data Source:** Windows Security Event Log

## 1. Objective

To verify that Windows user account creation events are recorded in the Security event log, forwarded to Wazuh, and identified by a Wazuh security rule.

## 2. Test Procedure

1. Checked the Windows User Account Management audit policy.
2. Confirmed that successful account-management auditing was enabled.
3. Verified the existence and current status of the test account `SOC-testuser`.
4. Queried the Windows Security log for Event ID 4720.
5. Searched for Event ID 4720 in Wazuh Discover.
6. Expanded the Wazuh event to inspect the detection rule and account details.

## 3. Evidence and Observations

### Windows Security Log

- Event ID: 4720
- Description: A user account was created.
- Created account: SOC-testuser
- Account domain: LAPTOP-FUSDRPR6
- Account creation time: 22 November 2026, 10:45:23
- Initiating account: LOQ

The Windows event recorded the creation of the local account.

### Wazuh Detection

The corresponding event was successfully found in Wazuh Discover.

- Agent name: Rosemary-Windows11
- Agent ID: 001
- Event ID: 4720
- Target username: SOC-testuser
- Rule description: User account enabled or created
- Rule ID: 60109
- Rule level: 8
- Rule fired times: 1

The rule groups included:

- windows
- windows_security
- adduser
- account_changed

## 4. Analysis

Windows Security Event ID 4720 provides evidence that a user account was created.

Wazuh successfully received the event and generated an alert using Rule ID 60109, with a severity level of 8.

The alert indicates a user-account management event that warrants review in a real security environment. Unexpected account creation can be relevant to investigations involving unauthorized account creation or persistence.

During this exercise, however, the account was intentionally created for laboratory testing. The event does not represent a confirmed security incident.

## 5. Conclusion

The user account creation monitoring exercise was successful.

The complete monitoring path was verified:

**Windows Security Log → Wazuh Agent → Wazuh Manager → Wazuh Discover**

The experiment demonstrates how a SOC analyst can identify new account creation and investigate the associated Wazuh alert.

## 6. Screenshot Evidence

- `04-Wazuh-User-Account-Creation-Detection.png`

**Investigation status:** Completed – successful event collection and alert generation.
