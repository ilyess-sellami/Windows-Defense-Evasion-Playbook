# 04 - AMSI Bypass Concepts

## Overview

The Anti-Malware Scan Interface (AMSI) is a Windows security feature that allows applications and scripting engines to submit content to security products for inspection before execution.

AMSI helps security solutions inspect potentially malicious content in PowerShell, VBScript, JavaScript, Office macros, and other scripting environments.

Because AMSI can reveal malicious content before execution, attackers often attempt to evade or interfere with AMSI inspection.

---

## AMSI Architecture

AMSI acts as an interface between applications and security products.

Typical AMSI workflow:

1. A script or command is submitted for execution.
2. The application sends the content to AMSI.
3. AMSI forwards the content to the installed security provider.
4. The security provider analyzes the content.
5. The content is either allowed or blocked.

Common AMSI-aware applications:

* PowerShell
* Windows Script Host (WSH)
* Microsoft Office VBA
* JScript
* VBScript

---

## Common AMSI Bypass Concepts

### 1. Script Obfuscation

Attackers may attempt to alter the appearance of scripts to avoid signature matching during AMSI inspection.

Examples include:

* String manipulation
* Encoding
* Variable substitution
* Dynamic command construction

Legitimate example of dynamic string construction:

```powershell
$service = "Win" + "Defend"
Get-Service $service
```

---

### 2. Runtime Content Generation

Instead of storing content directly in a script, content may be generated dynamically during execution.

Legitimate example:

```powershell
$path = Join-Path "C:\Windows" "System32"
Get-ChildItem $path
```

---

### 3. Reflection and Dynamic Execution Concepts

Some applications generate code dynamically at runtime.

Legitimate example:

```powershell
$scriptBlock = { Get-Process }
& $scriptBlock
```

Used legitimately for:

* Automation
* Administration
* Dynamic workflows

---

### 4. Encoded Content

Encoded data is frequently used in administrative and application workflows.

Legitimate example:

```powershell
$text = "Hello World"
$bytes = [System.Text.Encoding]::UTF8.GetBytes($text)
[Convert]::ToBase64String($bytes)
```

Common legitimate uses:

* Configuration storage
* Data transport
* API communication

---

### 5. In-Memory Execution Concepts

Modern applications frequently process data directly in memory.

Legitimate examples include:

* .NET applications
* PowerShell objects
* Application caches
* Browser memory

Because memory-based execution may reduce disk artifacts, it is often closely monitored by EDR solutions.