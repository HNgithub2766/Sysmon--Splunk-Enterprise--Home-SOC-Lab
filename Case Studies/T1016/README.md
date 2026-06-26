# T1016 - System Network Configuration Discovery

## Objective

Simulate network configuration discovery activity using Atomic Red Team to generate Windows and Sysmon telemetry, then develop and validate a Splunk detection for MITRE ATT&CK T1016.

---

## MITRE ATT&CK Mapping

* **Technique:** T1016 - System Network Configuration Discovery
* **Tactic:** Discovery

---

## Lab Environment

* Splunk Enterprise
* Sysmon
* Windows 11 VM
* Kali Linux VM
* Atomic Red Team
* VirtualBox

---

## Atomic Test Executed

```powershell
Invoke-AtomicTest T1016
```

The Atomic Red Team test executed multiple network configuration discovery commands including `ipconfig`, `netsh`, `arp`, `nbtstat`, `net config`, `route`, `nslookup` and firewall enumeration. Several advanced tests require an Active Directory environment, external payloads or additional dependencies and may not execute successfully in a standalone Windows lab. Overall, the test generated valuable Windows and Sysmon telemetry for developing and validating Splunk detections for MITRE ATT&CK T1016.

---

## Detection Logic

### Splunk Search

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
(Image="*\\ipconfig.exe" OR Image="*\\route.exe" OR Image="*\\arp.exe")
```

---

## Alert Configuration

| Setting        | Value                                          |
| -------------- | ---------------------------------------------- |
| Detection Name | T1016 - System Network Configuration Discovery |
| Severity       | Low                                            |
| Schedule       | Every Hour                                     |
| Trigger        | Results > 0                                    |
| Trigger Mode   | Once                                           |
| Throttle       | Enabled (every 60 mins)                        |
| Trigger Action | Add to Triggered Alerts                        |

---

## Sample Telemetry

```text
EventCode: 1
Image: C:\Windows\System32\ipconfig.exe
ComputerName: DESKTOP-QSSM57Q
LogSource: Microsoft-Windows-Sysmon/Operational
```

---

## Findings

* Successfully generated Sysmon Event ID 1 process creation events.
* Captured execution of network discovery commands including `ipconfig`, `arp`, `nbtstat`, `netsh`, `net config` and `nslookup`.
* Some Atomic tests requiring Active Directory, external payloads or Internet connectivity were not applicable to the lab environment.
* Detection successfully identified the generated telemetry within Splunk.
* Alert triggered as expected following execution of the Atomic Red Team simulation.

---

## Analysis

System Network Configuration Discovery enables attackers to understand the target's network environment, including IP addressing, routing information and neighbouring hosts. This information is commonly gathered during the reconnaissance phase before lateral movement or command-and-control communication.

---

## Detection Tuning

In a production environment, this detection would typically be correlated with other discovery techniques such as T1033 (System Owner/User Discovery) and T1082 (System Information Discovery). Administrative accounts and approved network management tools should be excluded where appropriate to reduce false positives.

---

## Screenshots

* Atomic Red Team execution
* Splunk detection query
* Triggered alert
* Representative Sysmon Event ID 1

---

## Lessons Learned

This exercise demonstrated how network discovery commands generate identifiable Windows telemetry that can be transformed into actionable Splunk detections and alerts. It also reinforced the importance of correlating multiple reconnaissance techniques to improve detection fidelity and reduce false positives.

