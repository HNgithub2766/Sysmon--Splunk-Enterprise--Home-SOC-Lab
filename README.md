## Overview

This project documents the development of a Home Security Operations Centre (SOC) lab built using Splunk Enterprise, Sysmon and Atomic Red Team. The purpose of the lab is to gain hands-on experience with security monitoring, detection engineering, alert development and log analysis commonly performed by SOC analysts and detection engineers.

The lab simulates a real-world security monitoring environment by collecting and analysing Windows Security and Sysmon telemetry generated through Atomic Red Team attack simulations. The focus of the project is to develop, test and tune security detections, create alerts and map observed activity to the MITRE ATT&CK framework.

---

## Objectives

* Gain hands-on experience with SIEM technologies.
* Develop familiarity with Windows Event Logs and Sysmon telemetry.
* Build and validate security detections using Splunk SPL.
* Develop and tune alerting logic to reduce false positives.
* Understand attacker tactics, techniques and procedures (TTPs).
* Map observed activity to the MITRE ATT&CK framework.
* Build practical SOC monitoring and detection engineering skills through simulated attack scenarios.

---

## Lab Environment

### Components

| Component | Purpose |
|-----------|---------|
| Splunk Enterprise | SIEM platform used for log collection, searching and alerting |
| Sysmon | Enhanced Windows telemetry and process monitoring |
| Windows 11 VM | Endpoint used to generate security events |
| Kali Linux VM | Attack simulation platform |
| Atomic Red Team | ATT&CK-based attack simulation framework |
| VirtualBox | Virtualisation platform hosting the lab environment |

### Log Sources 
* Windows Security Logs
* Sysmon Operational Logs
* Process Creation Events
* Network Connection Events
* Authentication Events
* PowerShell Activity
  
---

## Detection Engineering Workflow

1. Execute Atomic Red Team technique.
2. Generate telemetry within Windows and Sysmon.
3. Identify relevant events within Splunk.
4. Develop SPL detection logic.
5. Validate detection accuracy.
6. Create and configure Splunk alerts.
7. Tune detections to reduce false positives.
8. Map detections to MITRE ATT&CK techniques.
9. Document findings and lessons learned.

---

## Example Detection Use Cases

Each detection includes:

* Attack simulation
* Relevant Sysmon or Windows event IDs
* Splunk detection query
* Alert configuration
* MITRE ATT&CK mapping
* Detection tuning recommendations
* Screenshots of generated telemetry and alert results

---

## Detection Use Cases

The following detections are being developed and validated using Sysmon telemetry, Splunk SPL and Atomic Red Team simulations.

### T1033 - System Owner/User Discovery

Detection of user enumeration and discovery activity through commands such as:

```cmd
whoami
net user
query user
```

**Data Sources**

* Sysmon Event ID 1 (Process Creation)

**MITRE ATT&CK**

* T1033 - System Owner/User Discovery

---

### T1110 - Brute Force

Detection of repeated failed authentication attempts.

**Data Sources**

* Windows Security Event ID 4625

**MITRE ATT&CK**

* T1110 - Brute Force

---

### T1059.001 - PowerShell

Detection of PowerShell execution and potentially suspicious command activity.

**Data Sources**

* Sysmon Event ID 1
* PowerShell Operational Logs

**MITRE ATT&CK**

* T1059.001 - PowerShell

---

### T1082 - System Information Discovery

Detection of host reconnaissance commands such as:

```cmd
systeminfo
hostname
wmic
```

**Data Sources**

* Sysmon Event ID 1

**MITRE ATT&CK**

* T1082 - System Information Discovery

---

### T1016 - System Network Configuration Discovery

Detection of network discovery activity through commands such as:

```cmd
ipconfig /all
route print
arp -a
```

**Data Sources**

* Sysmon Event ID 1

**MITRE ATT&CK**

* T1016 - System Network Configuration Discovery

---

### T1105 - Ingress Tool Transfer

Detection of file downloads and tool transfers to a compromised host.

Examples include:

```powershell
Invoke-WebRequest
curl
certutil
```

**Data Sources**

* Sysmon Event ID 1 (Process Creation)
* Sysmon Event ID 3 (Network Connections)

**MITRE ATT&CK**

* T1105 - Ingress Tool Transfer

---

### T1003 - OS Credential Dumping

Detection of attempts to access or dump credentials from memory.

Examples include:

```cmd
procdump.exe
mimikatz.exe
rundll32.exe
```

**Data Sources**

* Sysmon Event ID 1 (Process Creation)
* Sysmon Event ID 10 (Process Access)

**MITRE ATT&CK**

* T1003 - OS Credential Dumping


## Skills Developed

* Detection Engineering
* SIEM Administration
* Splunk Search Processing Language (SPL)
* Windows Event Log Analysis
* Sysmon Log Analysis
* Security Monitoring
* Alert Development and Tuning
* Threat Detection
* MITRE ATT&CK Mapping
* Security Documentation
* Atomic Red Team Attack Simulation

---

## Current Status

Project currently in progress.

Planned enhancements include:

* Additional detection rules
* Correlation searches
* Alert tuning and false positive reduction
* Dashboard development
* Threat hunting exercises
* Microsoft Sentinel integration
* Expanded Atomic Red Team coverage

