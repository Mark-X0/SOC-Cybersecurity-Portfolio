# 09 — Persistence via Backdoor Account Creation

## 1. Attack Overview

Creating an additional user account can be abused by an attacker to maintain access to a compromised Windows system.

In this scenario, a local account named `hacker` was created on the Windows target and added to the local Administrators group.

This simulated a persistence technique in which an attacker creates an unauthorized privileged account to retain administrative access.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Persistence
- **Technique:** T1136 — Create Account
- **Sub-technique:** T1136.001 — Create Account: Local Account

## 3. Attack Simulation

The native Windows `net user` and `net localgroup` commands were used to create a local account and assign it administrative privileges.

Example command structure:

```cmd
net user hacker <PASSWORD> /add
net localgroup Administrators hacker /add
```

**Command explanation:**

- `net user hacker <PASSWORD> /add`: Creates a local account named `hacker`.
- `net localgroup Administrators hacker /add`: Adds the account to the local Administrators group.

The account was created as part of the isolated lab simulation.

## 4. Detection & Investigation

Windows Security auditing was used to monitor account creation and group membership changes.

The relevant Windows Security events were:

- **Event ID 4720 — A user account was created.**
- **Event ID 4732 — A member was added to a security-enabled local group.**

Event ID 4720 provides evidence of account creation, while Event ID 4732 records the addition of a member to a local security-enabled group.

Together, these events help analysts identify suspicious account creation followed by privilege assignment.

## 5. Wazuh Alert Evidence

The Windows Server Wazuh Agent forwarded the account-management events to the Wazuh Manager.

The Wazuh Dashboard was used to review the account creation and local Administrators group modification activity.

The investigation focused on:

- Event ID 4720 and the newly created account.
- Event ID 4732 and the group membership change.
- The account responsible for the changes, when available.
- The event timestamps and associated alert details.

Correlating both events provides stronger evidence of a potentially unauthorized privileged account than reviewing account creation alone.
