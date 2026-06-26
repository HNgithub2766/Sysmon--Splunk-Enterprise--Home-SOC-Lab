# T1059.001 - PowerShell

## Objective

Simulate PowerShell execution using Atomic Red Team to generate Windows and Sysmon telemetry, then develop and validate a Splunk detection for MITRE ATT&CK T1059.001.

---

## MITRE ATT&CK Mapping

* **Technique:** T1059.001 - PowerShell
* **Tactic:** Execution

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
Invoke-AtomicTest T1059.001
```

The Atomic Red Team test executed multiple PowerShell commands and scripts to simulate attacker behaviour. Several advanced tests required additional dependencies, Internet connectivity or elevated privileges and may not execute successfully in a standalone Windows lab. Overall, the test generated valuable Windows and Sysmon telemetry for developing and validating Splunk detections for MITRE ATT&CK T1059.001.

---

## Detection Logic

### Splunk Search

```spl
source="WinEventLog:Microsoft-Windows-Sysmon/Operational"
EventCode=1
Image="*\\powershell.exe"
(CommandLine="*-enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*IEX*" OR CommandLine="*Invoke-Expression*")
```

---

## Alert Configuration

| Setting        | Value                   |
| -------------- | ----------------------- |
| Detection Name | T1059.001 - PowerShell  |
| Severity       | Low                     |
| Schedule       | Every Hour              |
| Trigger        | Results > 0             |
| Trigger Mode   | Once                    |
| Throttle       | Enabled (1 Hour)        |
| Trigger Action | Add to Triggered Alerts |

---

## Sample Telemetry

```text
EventCode: 1
Image: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
ComputerName: DESKTOP-QSSM57Q
LogSource: Microsoft-Windows-Sysmon/Operational
```

---

## Findings

* Successfully generated Sysmon Event ID 1 process creation events.
* Captured execution of PowerShell with suspicious command-line arguments.
* Detection successfully identified the generated telemetry within Splunk.
* Alert triggered as expected following execution of the Atomic Red Team simulation.

---

## Analysis

PowerShell is frequently abused by attackers to execute malicious commands, download payloads and perform fileless attacks. Monitoring encoded commands and execution techniques such as `Invoke-Expression (IEX)` provides visibility into potentially malicious PowerShell activity.

---

## Detection Tuning

In a production environment, this detection should be tuned to exclude known administrative scripts and trusted automation tools. Additional indicators such as parent processes, network connections and encoded command execution should be correlated to improve detection fidelity and reduce false positives.

---

## Screenshots

* Atomic Red Team execution
* Splunk detection query
* Triggered alert
* Representative Sysmon Event ID 1

---

## Lessons Learned

This exercise demonstrated how PowerShell execution generates identifiable Windows telemetry that can be transformed into actionable Splunk detections and alerts. It also highlighted the importance of monitoring suspicious PowerShell command-line arguments commonly associated with attacker tradecraft.

