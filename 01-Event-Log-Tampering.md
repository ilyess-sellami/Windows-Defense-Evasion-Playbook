# 01 - Event Log Tampering (Windows Defense Evasion)

## Overview

Event Log Tampering refers to techniques used to interfere with Windows logging mechanisms in order to reduce visibility of malicious activity. Attackers may attempt to delete logs, disable logging services, or manipulate log generation to hinder forensic investigations.

---

## Windows Event Log Architecture

Key log sources in Windows:

* Security Logs (authentication, privilege use)
* System Logs (drivers, services, system events)
* Application Logs (software events)
* PowerShell Operational Logs
* Windows Defender Logs

Event logs are managed by the **Windows Event Log Service (eventlog)** and stored in `.evtx` format.

---

## Common Event Log Tampering Techniques (Conceptual)

### 1. Clearing Event Logs

Attackers may attempt to erase logs to remove evidence of execution.

#### Example Commands

```powershell
wevtutil cl System
wevtutil cl Security
wevtutil cl Application
```

```cmd
Clear-EventLog -LogName Security
```

---

### 2. Disabling Event Log Service

Stopping or disabling logging services reduces visibility.

```cmd
sc stop eventlog
sc config eventlog start= disabled
```

---

### 3. Log File Deletion (Offline Tampering)

Direct deletion of `.evtx` files (requires elevated privileges).

Typical locations:

```
C:\Windows\System32\winevt\Logs\
```

---

### 4. Selective Log Manipulation

Instead of full deletion, attackers may attempt:

* Removing specific event IDs (rare in practice)
* Time manipulation (system clock changes)
* Log flooding (noise generation to hide activity)
