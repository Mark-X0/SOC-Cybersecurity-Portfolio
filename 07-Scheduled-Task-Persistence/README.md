# 07 — Persistence via Scheduled Task

## 1. Attack Overview

Scheduled Tasks are a legitimate Windows feature used to execute programs or scripts automatically at predefined times or in response to specific triggers.

Attackers may abuse this feature to maintain persistence on a compromised system by creating tasks that execute automatically.

In this scenario, a scheduled task named `WindowsUpdateCheck` was created to simulate a persistence mechanism on the Windows Server target.

The task was configured to run with SYSTEM privileges when a user logged on.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Persistence
- **Technique:** T1053 — Scheduled Task/Job
- **Sub-technique:** T1053.005 — Scheduled Task

## 3. Attack Simulation

The Windows `schtasks` utility was used to create the scheduled task.

Example command structure:

```cmd
schtasks /create /tn "WindowsUpdateCheck" /tr "<COMMAND_OR_SCRIPT>" /sc onlogon /ru SYSTEM
```

**Command explanation:**

- `/create`: Creates a new scheduled task.
- `/tn`: Specifies the task name.
- `/tr`: Specifies the program or command to execute.
- `/sc onlogon`: Configures the task to run when a user logs on.
- `/ru SYSTEM`: Configures the task to run under the SYSTEM account.

The task name was chosen to resemble a legitimate Windows update-related task.

## 4. Detection & Investigation

Windows Security auditing was used to monitor scheduled task creation.

The relevant Windows Security event was:

- **Event ID 4698 — A scheduled task was created.**

This event can provide details about the newly created task, including its name and task definition when available.

During investigation, analysts should review the task name, executable or script path, trigger, execution account, and creation time.

## 5. Wazuh Alert Evidence

The Windows Server Wazuh Agent forwarded the relevant Security events to the Wazuh Manager.

The Wazuh Dashboard was used to review the scheduled task creation activity.

The investigation focused on:

- Event ID 4698.
- The task name `WindowsUpdateCheck`.
- The configured execution account.
- The task trigger and command details, when available.

This helped demonstrate how Windows auditing can provide visibility into persistence-related activity.
