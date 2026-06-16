# Splunk SIEM & Sysmon Home SOC Lab

## Overview

This project documents the development of a Home Security Operations Centre (SOC) lab built using Splunk Enterprise and Sysmon. The purpose of the lab is to gain hands-on experience with security monitoring, log analysis, alert investigation and incident response processes commonly used by SOC analysts.

The lab simulates a real-world security monitoring environment by collecting and analysing Windows security events and Sysmon telemetry. It is designed to support practical learning around threat detection, security investigations and MITRE ATT&CK mapping.

---

## Objectives

* Gain hands-on experience with SIEM technologies.
* Develop familiarity with Windows event logging and Sysmon telemetry.
* Practice log analysis and alert investigation.
* Understand attacker tactics, techniques and procedures (TTPs).
* Map detected activity to the MITRE ATT&CK framework.
* Build practical SOC analyst skills through simulated attack scenarios.

---

## Lab Environment

### Components

| Component         | Purpose                                                            |
| ----------------- | ------------------------------------------------------------------ |
| Splunk Enterprise | SIEM platform used for log collection, searching and investigation |
| Sysmon            | Enhanced Windows event logging                                     |
| Windows 11 VM     | Endpoint used to generate security events                          |
| VirtualBox        | Virtualisation platform hosting the lab environment                |
| Kali Linux VM     | Attack Simulation platform 

### Log Sources

* Windows Security Logs
* Sysmon Operational Logs
* Process Creation Events
* Network Connection Events
* Authentication Events
* PowerShell Activity

---

## Security Monitoring Activities

### Event Monitoring

The lab is configured to monitor:

* User logon and logoff activity
* Failed authentication attempts
* Account management events
* Process creation activity
* PowerShell execution
* Network connections
* Service creation events

### Investigation Workflow

1. Alert or suspicious activity identified.
2. Review relevant logs within Splunk.
3. Analyse associated processes, users and hosts.
4. Determine potential malicious behaviour.
5. Map activity to MITRE ATT&CK techniques.
6. Document findings and remediation recommendations.

---

## Example Detection Use Cases

### Account Enumeration

Detection of commands such as:

```cmd
whoami
net user
query user
```

MITRE ATT&CK:

* T1033 – System Owner/User Discovery

---

### Failed Login Monitoring

Detection of excessive failed authentication attempts.

MITRE ATT&CK:

* T1110 – Brute Force

---

### Suspicious PowerShell Activity

Monitoring PowerShell execution for potentially malicious commands.

MITRE ATT&CK:

* T1059.001 – PowerShell

---

### Process Creation Monitoring

Monitoring unusual or suspicious process execution using Sysmon Event ID 1.

MITRE ATT&CK:

* T1055 – Process Injection
* T1059 – Command and Scripting Interpreter

---

## Skills Developed

* SIEM Administration
* Splunk Search Processing Language (SPL)
* Windows Event Log Analysis
* Sysmon Log Analysis
* Security Monitoring
* Alert Triage
* Incident Investigation
* Threat Detection
* MITRE ATT&CK Mapping
* Security Documentation

---

## Current Status

Project currently in progress.

Planned enhancements include:

* Additional detection rules
* Dashboard development
* Threat hunting exercises
* Microsoft Sentinel integration
* Atomic Red Team attack simulations

---

## Disclaimer

This lab is used solely for educational and defensive security purposes within an isolated virtual environment.
