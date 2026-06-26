# T1082 - System Information Discovery

## Objective

Simulate system information discovery activity using Atomic Red Team to generate Windows and Sysmon telemetry, then develop and validate a Splunk detection for MITRE ATT&CK T1082.

---

## MITRE ATT&CK

* **Technique:** T1082 - System Information Discovery
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
Invoke-AtomicTest T1082
```

The Atomic Red Team test executed multiple system discovery commands to enumerate host information including the hostname, operating system version, BIOS information, environment variables, registry values and hardware details. Several advanced reconnaissance tests were blocked by Microsoft Defender or failed due to missing dependencies, which is expected within a standard Windows lab environment.

---

## Detection Logic

### Splunk Search

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
(
Image="*\\systeminfo.exe"
OR Image="*\\hostname.exe"
OR Image="*\\wmic.exe"
OR Image="*\\reg.exe"
OR Image="*\\vssadmin.exe"
OR CommandLine="*Get-WmiObject*"
OR CommandLine="*Get-ComputerInfo*"
OR CommandLine="*gdr*"
)
```

---

## Alert Configuration

| Setting        | Value                                |
| -------------- | ------------------------------------ |
| Detection Name | T1082 - System Information Discovery |
| Severity       | Low                                  |
| Schedule       | Every Hour                           |
| Trigger        | Results > 0                          |
| Trigger Mode   | For Each Result                      |
| Throttle       | Disabled                             |
| Trigger Action | Add to Triggered Alerts              |

---

## Sample Telemetry

```text
EventCode: 1
Image: C:\Windows\System32\systeminfo.exe
ComputerName: DESKTOP-QSSM57Q
LogSource: Microsoft-Windows-Sysmon/Operational
```

---

## Findings

* Successfully generated Sysmon Event ID 1 process creation events.
* Captured execution of system discovery commands including `systeminfo`, `hostname`, `wmic` and registry queries.
* Detection successfully identified the generated telemetry within Splunk.
* Alert triggered as expected following execution of the Atomic Red Team simulation.

---

## Analysis

System Information Discovery is commonly performed by attackers after gaining initial access to understand the operating environment before privilege escalation or lateral movement. Monitoring execution of reconnaissance commands provides valuable visibility into early-stage attacker behaviour.

---

## Detection Tuning

In a production environment, this detection would typically be correlated with additional discovery techniques such as T1033 (System Owner/User Discovery) and T1016 (System Network Configuration Discovery) to reduce false positives and improve detection fidelity.

---

## Screenshots

* Atomic Red Team execution
* Splunk detection query
* Triggered alert
* Representative Sysmon Event ID 1

---

## Lessons Learned

This exercise demonstrated how attacker reconnaissance activity generates identifiable Windows telemetry that can be transformed into actionable Splunk detections and alerts. It also highlighted the importance of tuning detections to distinguish legitimate administrative activity from potentially malicious reconnaissance.

