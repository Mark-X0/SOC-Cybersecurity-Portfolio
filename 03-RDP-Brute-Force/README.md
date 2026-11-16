# 03 — RDP Brute Force

## 1. Attack Overview

Remote Desktop Protocol (RDP) is commonly used to access Windows systems remotely. If exposed and protected by weak credentials, it may become a target for password-guessing attacks.

In this scenario, Hydra was used from Kali Linux to perform repeated RDP authentication attempts against the Windows Server target.

The objective was to test Windows authentication monitoring and verify whether failed remote logon attempts could be identified through Wazuh.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Credential Access
- **Technique:** T1110 — Brute Force
- **Sub-technique:** T1110.001 — Password Guessing

## 3. Attack Simulation

The attack was performed using Hydra:

```bash
hydra -l administrator -P <WORDLIST> rdp://<TARGET_IP>
```

**Command explanation:**

- `-l administrator`: Specifies the username being targeted.
- `-P <WORDLIST>`: Specifies the password list.
- `rdp://<TARGET_IP>`: Identifies the target RDP service.

The tool attempted multiple authentication combinations against the RDP service.

## 4. Detection & Investigation

Windows Security auditing was used to monitor authentication attempts on the target server.

Failed RDP logon attempts were recorded in the Windows Security Event Log.

The relevant event was:

- **Event ID 4625 — An account failed to log on.**

The Windows Server Wazuh Agent forwarded the collected security events to the Wazuh Manager for centralized monitoring and investigation.

## 5. Wazuh Alert Evidence

The Wazuh Dashboard was used to review the authentication failure activity.

The investigation focused on:

- Failed logon events.
- The targeted account.
- The source address, when available in the event.
- The event timestamp and associated alert details.

Event ID 4625 provides evidence of failed authentication, but repeated events and their context are needed to distinguish a brute-force attempt from ordinary login mistakes.

