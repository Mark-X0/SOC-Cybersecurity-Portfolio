# 06 — Obfuscated PowerShell Execution

## 1. Attack Overview

PowerShell is a legitimate Windows administration and automation tool. However, attackers may abuse it to execute commands while using obfuscation techniques to make their activity harder to understand during initial inspection.

In this scenario, a Base64-encoded PowerShell command was executed on the Windows Server target to simulate obfuscated command execution.

The objective was to verify whether PowerShell activity could be captured and investigated through Windows logging and Sysmon telemetry.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Defense Evasion
- **Technique:** T1027 — Obfuscated Files or Information
- **Additional Technique:** T1059.001 — PowerShell

## 3. Attack Simulation

A Base64-encoded PowerShell command was used to simulate obfuscated execution.

PowerShell supports encoded command execution through the `-EncodedCommand` parameter.

Example format:

```powershell
powershell.exe -EncodedCommand <BASE64_COMMAND>
```

**Command explanation:**

- `powershell.exe`: Starts the Windows PowerShell process.
- `-EncodedCommand`: Executes a command supplied as a Base64-encoded string.
- `<BASE64_COMMAND>`: Represents the encoded command used in the lab.

The encoded command was used to simulate an execution pattern that may require additional investigation to understand.

## 4. Detection & Investigation

PowerShell Script Block Logging was enabled to record script content processed by PowerShell.

The relevant Windows event was:

- **Event ID 4104 — PowerShell Script Block Logging.**

This event can provide visibility into the script block content, helping analysts investigate commands even when an encoded command-line argument was used.

Sysmon telemetry was also used to monitor process and file activity. In this scenario, Sysmon recorded PowerShell-related activity involving the creation of a scripting file in a temporary directory.

## 5. Wazuh Alert Evidence

The Windows Server Wazuh Agent forwarded relevant Windows and Sysmon events to the Wazuh Manager.

The investigation focused on:

- PowerShell execution activity.
- Event ID 4104 and its recorded script-block content.
- The PowerShell process and associated file activity.
- The temporary-directory activity observed in Sysmon.

These sources provide complementary visibility into command execution and related host activity.
