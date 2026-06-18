# 03 - PowerShell Obfuscation

## Overview

PowerShell Obfuscation refers to techniques used to disguise PowerShell commands, scripts, and payload delivery in order to bypass detection mechanisms such as signature-based antivirus, AMSI (Anti-Malware Scan Interface), and script logging systems.

Because PowerShell is a powerful built-in administration tool in Windows, it is frequently abused in post-exploitation and red team operations.

---

## Why PowerShell is Targeted

PowerShell is heavily monitored due to its capabilities:

* System administration and automation
* File and registry manipulation
* Network communication
* In-memory execution
* Integration with .NET framework

Defenders often rely on:

* Script Block Logging
* AMSI inspection
* Constrained Language Mode
* EDR behavioral detection

---

## Common PowerShell Obfuscation Techniques

### 1. String Concatenation

**Normal legitimate usage:**

PowerShell allows building strings dynamically for automation tasks.

```powershell
$path = "C:" + "\Windows" + "\System32"
Get-ChildItem $path
```

Used legitimately for:

* Dynamic path construction
* Flexible scripting

---

### 2. Base64 Encoding

**Legitimate use case:**

Base64 is often used for encoding data transmission or storing binary-safe content.

```powershell
$bytes = [System.Text.Encoding]::UTF8.GetBytes("Hello World")
$encoded = [Convert]::ToBase64String($bytes)
$encoded
```

And decoding:

```powershell
[System.Text.Encoding]::UTF8.GetString([Convert]::FromBase64String($encoded))
```

Used for:

* Data encoding
* Configuration transfer
* API communication

---

### 3. Character Substitution

**Legitimate use case:**

Casting characters is sometimes used in scripting or parsing.

```powershell
[char]72 + [char]73
```

Used for:

* Low-level text processing
* Educational scripting

---

### 4. Variable Usage for Commands

**Legitimate use case:**

Storing commands or values in variables is standard scripting practice.

```powershell
$cmd = "Get-Process"
Invoke-Expression $cmd
```

Used for:

* Dynamic automation workflows
* Script modularity (though Invoke-Expression is generally discouraged in secure environments)

---

### 5. Dynamic Invocation

**Legitimate use case:**

PowerShell supports dynamic execution in admin automation scenarios.

```powershell
$script = { Get-Service }
& $script
```

Used for:

* Job scheduling
* Remote automation
* Script blocks in administration

---

### 6. Whitespace and Formatting

**Legitimate use case:**

Whitespace flexibility is part of PowerShell syntax.

```powershell
Get-ChildItem   -Path   "C:\Windows"
```

Used for:

* Readability adjustments
* Script formatting variations

---

### 7. Script Structure Modification

**Legitimate use case:**

Splitting logic into multiple parts for maintainability.

```powershell
function Get-SystemInfo {
    Get-ComputerInfo
}

Get-SystemInfo
```

Used for:

* Modular scripting
* Reusable automation functions