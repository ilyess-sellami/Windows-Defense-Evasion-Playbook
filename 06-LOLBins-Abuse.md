# 06 - LOLBins Abuse

## Overview

Living Off The Land Binaries (LOLBins) are legitimate Microsoft-signed executables that are included with Windows and commonly used for administration, troubleshooting, and system management.

Because these binaries are trusted and frequently executed in enterprise environments, attackers may abuse them to blend malicious activity with normal system operations.

LOLBins are frequently observed during red team engagements, penetration tests, and real-world intrusions.

---

## What Makes LOLBins Attractive

LOLBins provide several advantages:

* Already present on Windows systems
* Signed by Microsoft
* Often trusted by security controls
* Commonly used by administrators
* May bypass application allowlisting policies

Common examples include:

* `powershell.exe`
* `cmd.exe`
* `rundll32.exe`
* `regsvr32.exe`
* `mshta.exe`
* `certutil.exe`
* `wmic.exe`
* `schtasks.exe`

---

## Common LOLBin Abuse Scenarios

## 1. PowerShell

PowerShell is a legitimate administration framework.

Legitimate example:

```powershell
Get-Service
```

Common administrative uses:

* System management
* Automation
* Remote administration
* Configuration management

---

### 2. Certutil

Certutil is a Windows certificate management utility.

Legitimate example:

```cmd
certutil -store My
```

Common administrative uses:

* Certificate management
* PKI troubleshooting
* Certificate validation

---

### 3. Rundll32

Rundll32 allows Windows to execute functions contained within DLL files.

Legitimate example:

```cmd
rundll32.exe shell32.dll,Control_RunDLL
```

Common administrative uses:

* Launching Control Panel applets
* Executing DLL-based functionality
* Legacy Windows operations

---

### 4. Regsvr32

Regsvr32 registers and unregisters COM components.

Legitimate example:

```cmd
regsvr32.exe mycomponent.dll
```

Common administrative uses:

* Software installation
* COM registration
* Application troubleshooting

---

### 5. MSHTA

MSHTA executes Microsoft HTML Applications (.hta files).

Legitimate example:

```cmd
mshta.exe C:\Scripts\AdminTool.hta
```

Common administrative uses:

* Internal administrative tools
* Legacy enterprise applications
* GUI-based automation

---

### 6. WMIC

WMIC provides command-line access to Windows Management Instrumentation (WMI).

Legitimate example:

```cmd
wmic process list brief
```

Common administrative uses:

* Asset inventory
* System information gathering
* Remote administration

---

### 7. Schtasks

Schtasks manages scheduled tasks on Windows.

Legitimate example:

```cmd
schtasks /query
```

Common administrative uses:

* Task automation
* Maintenance jobs
* Scheduled monitoring