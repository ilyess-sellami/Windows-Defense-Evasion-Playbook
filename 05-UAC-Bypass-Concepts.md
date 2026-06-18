# 05 - UAC Bypass Concepts

## Overview

User Account Control (UAC) is a Windows security feature designed to limit the impact of administrative privileges by requiring consent or credentials before performing sensitive actions.

Even when a user belongs to the local Administrators group, applications typically run with standard user privileges until elevated.

Because UAC can interrupt malicious activity and increase visibility, attackers often attempt to bypass or abuse elevation mechanisms.

---

## UAC Architecture

UAC works by separating:

* Standard user privileges
* Administrative privileges

When elevation is required:

1. An application requests elevated privileges.
2. Windows displays a UAC prompt.
3. The user approves or denies the request.
4. The process runs with elevated rights if approved.

Common integrity levels:

* Low Integrity
* Medium Integrity
* High Integrity
* System Integrity

---

## Common UAC Bypass Concepts

### 1. Auto-Elevated Applications

Some Windows components are designed to run with elevated privileges without displaying a prompt under specific conditions.

Legitimate example:

```cmd
control.exe
```

Common administrative uses:

* Opening Control Panel
* Managing system settings
* Launching administrative tools

---

### 2. Administrative Tools

Windows includes many built-in administrative utilities that require elevation.

Legitimate examples:

```cmd
compmgmt.msc
```

```cmd
services.msc
```

```cmd
eventvwr.msc
```

Common administrative uses:

* Managing services
* Viewing logs
* System administration

---

### 3. Registry-Based Configuration

Administrative tools often interact with the Windows Registry.

Legitimate example:

```cmd
reg query HKLM\SOFTWARE
```

Common administrative uses:

* Software configuration
* System auditing
* Troubleshooting

---

### 4. Elevated Process Creation

Administrators frequently launch applications with elevated privileges.

Legitimate PowerShell example:

```powershell
Start-Process notepad.exe -Verb RunAs
```

Common administrative uses:

* Software installation
* Configuration changes
* System maintenance

---

### 5. Scheduled Administrative Tasks

Windows can execute administrative actions through Task Scheduler.

Legitimate example:

```cmd
schtasks /query
```

Common administrative uses:

* Backups
* Maintenance operations
* Automated monitoring

---

### 6. Microsoft Management Console (MMC)

MMC hosts many administrative snap-ins.

Legitimate examples:

```cmd
gpedit.msc
```

```cmd
devmgmt.msc
```

Common administrative uses:

* Group Policy management
* Device administration
* Security configuration
