# T1033 - System Owner/User Discovery

## Objective

Simulate user discovery activity using Atomic Red Team to generate Windows and Sysmon telemetry, then develop and validate a Splunk detection for MITRE ATT&CK T1033.

---

## MITRE ATT&CK Mapping

* **Technique:** T1033 - System Owner/User Discovery
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
Invoke-AtomicTest T1033
```

The Atomic Red Team test executed multiple user discovery commands to enumerate the currently logged-on user, local accounts and active user sessions. Some advanced discovery tests failed due to missing dependencies or permission restrictions, which is expected within a standalone Windows lab environment.

---

## Detection Logic

### Splunk Search

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
(Image="*\\whoami.exe" OR CommandLine="*whoami*")
```

---

## Alert Configuration

| Setting        | Value                               |
| -------------- | ----------------------------------- |
| Detection Name | T1033 - System Owner/User Discovery |
| Severity       | Low                                 |
| Schedule       | Every Hour                          |
| Trigger        | Results > 0                         |
| Trigger Mode   | For Each Result                     |
| Throttle       | Disabled                            |
| Trigger Action | Add to Triggered Alerts             |

---

## Sample Telemetry

```text
EventCode: 1
Image: C:\Windows\System32\whoami.exe
ProcessId: 4912
ComputerName: DESKTOP-QSSM57Q
LogSource: Microsoft-Windows-Sysmon/Operational
```

---

## Findings

* Successfully generated Sysmon Event ID 1 process creation events.
* Captured execution of `whoami.exe` and additional user discovery commands.
* Detection successfully identified the generated telemetry within Splunk.
* Alert triggered as expected following execution of the Atomic Red Team simulation.

---

## Analysis

System Owner/User Discovery is commonly performed immediately after initial access to determine the current security context and privilege level. Monitoring execution of user discovery commands provides visibility into attacker reconnaissance during the early stages of an intrusion.

---

## Detection Tuning

In a production environment, this detection would typically be correlated with additional discovery techniques such as T1082 (System Information Discovery) and T1016 (System Network Configuration Discovery). Known administrative accounts and approved management tools would also be excluded to reduce false positives.

---

## Screenshots

* Atomic Red Team execution
* Splunk detection query
* Triggered alert
* Representative Sysmon Event ID 1

---

## Lessons Learned

This exercise demonstrated how user discovery commands generate identifiable Windows telemetry that can be transformed into actionable Splunk detections and alerts. It also highlighted the importance of correlating reconnaissance techniques and tuning detections to reduce false positives in production environments.





