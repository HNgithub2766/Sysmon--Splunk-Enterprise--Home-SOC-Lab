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

### Components

| Component | Purpose |
|-----------|---------|
| Splunk Enterprise | SIEM platform used for log collection, searching and alerting |
| Sysmon | Enhanced Windows telemetry and process monitoring |
| Windows 11 VM | Endpoint used to generate security events |
| Kali Linux VM | Attack simulation platform |
| Atomic Red Team | ATT&CK-based attack simulation framework |
| VirtualBox | Virtualisation platform hosting the lab environment |

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

