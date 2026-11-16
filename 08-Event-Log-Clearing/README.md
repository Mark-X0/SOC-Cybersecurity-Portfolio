# 08 — Defense Evasion: Clearing Windows Event Logs

## 1. Attack Overview

Windows Event Logs contain valuable information about system activity, authentication, security events, and administrative actions.

An attacker may attempt to clear these logs to remove evidence of previous activity and make incident investigation more difficult.

In this scenario, the Windows Security event log was cleared on the target system to simulate a defense-evasion technique.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Defense Evasion
- **Technique:** T1070 — Indicator Removal
- **Sub-technique:** T1070.001 — Clear Windows Event Logs

## 3. Attack Simulation

The native Windows `wevtutil` utility was used to clear the Security event log:

```cmd
wevtutil cl Security
```

**Command explanation:**

- `wevtutil`: Windows command-line utility for managing event logs.
- `cl`: Clears the specified event log.
- `Security`: Specifies the Windows Security event log.

This activity was performed in the isolated lab environment to test security-event monitoring.

## 4. Detection & Investigation

Windows Security auditing records an event when the Security audit log is cleared.

The relevant event was:

- **Event ID 1102 — The audit log was cleared.**

This event is particularly important because clearing the Security log can remove records that would otherwise support an investigation.

The event itself provides evidence that the Security audit log was cleared, while its timestamp and account information can help analysts investigate who performed the action and when.

## 5. Wazuh Alert Evidence

The Windows Server Wazuh Agent forwarded the available security event to the Wazuh Manager.

The Wazuh Dashboard was used to identify the log-clearing activity and review the corresponding alert.

The investigation focused on:

- Event ID 1102.
- The account associated with the action, when available.
- The event timestamp.
- The corresponding Wazuh alert details.

The detection demonstrates the importance of monitoring security-log manipulation rather than relying only on the logs themselves.
