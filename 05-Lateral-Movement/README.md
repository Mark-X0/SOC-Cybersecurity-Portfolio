# 05 — Lateral Movement via Windows Remote Management

## 1. Attack Overview

Lateral Movement refers to techniques used by an attacker to access additional systems or resources after obtaining an initial foothold.

In this scenario, Evil-WinRM was used from Kali Linux to establish a remote PowerShell session with the Windows Server Domain Controller using compromised domain-user credentials.

The scenario demonstrates how valid credentials can be abused to access a remote Windows system through Windows Remote Management (WinRM).

## 2. MITRE ATT&CK Mapping

- **Tactic:** Lateral Movement
- **Technique:** T1021 — Remote Services
- **Sub-technique:** T1021.006 — Windows Remote Management

## 3. Attack Simulation

The remote session was initiated using Evil-WinRM:

```bash
evil-winrm -i <TARGET_IP> -u <DOMAIN_USER> -p '<PASSWORD>'
```

**Command explanation:**

- `-i <TARGET_IP>`: Specifies the target Windows host.
- `-u <DOMAIN_USER>`: Specifies the domain username.
- `-p '<PASSWORD>'`: Supplies the password used for authentication.

A remote PowerShell session was established using the compromised domain-user credentials.

## 4. Detection & Investigation

Windows Security auditing was used to monitor remote authentication activity on the target server.

The relevant event observed during the lab was:

- **Event ID 4624 — An account was successfully logged on.**
- **Logon Type 3 — Network logon.**

This event provided evidence of a successful network authentication.

During investigation, the account name, source address, timestamp, and available authentication details can help establish whether the remote session was expected or suspicious.

## 5. Wazuh Alert Evidence

The Windows Server Wazuh Agent forwarded the security events to the Wazuh Manager.

The Wazuh Dashboard provided centralized visibility into the successful remote logon activity.

The investigation focused on:

- The account used to establish the remote session.
- The successful logon event.
- Logon Type 3.
- The source address and timestamp, when available.

A successful logon by itself does not prove malicious lateral movement. Its context and relationship to the simulated activity are important.

