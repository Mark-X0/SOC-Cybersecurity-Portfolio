# Key Learnings & SOC Investigation Insights

## 1. Project Overview

Building and testing this SOC home lab provided practical experience in simulating attack techniques, collecting security telemetry, analyzing events, and validating detection capabilities through centralized monitoring.

The scenarios helped demonstrate how different security data sources can contribute to identifying suspicious activities across network traffic, Windows endpoints, and Active Directory.

## 2. Network Monitoring & Threat Detection

Using Suricata IDS provided practical exposure to network-based threat detection.

Key takeaways:

- Understanding how reconnaissance activities such as port scanning appear in network traffic.
- Using custom detection rules to identify suspicious scanning behavior.
- Reviewing IDS alerts and understanding the information they provide.
- Integrating network detection visibility into a centralized monitoring workflow.

## 3. Windows Security Monitoring

Monitoring Windows Server events provided insight into how operating-system auditing supports security investigations.

Important events explored during the lab included:

| Event ID | Description | Security Relevance |
|---|---|---|
| 4624 | Successful logon | Investigating successful authentication |
| 4625 | Failed logon | Identifying repeated authentication failures |
| 4698 | Scheduled task created | Detecting potential persistence |
| 4720 | User account created | Monitoring account creation |
| 4732 | Member added to a security-enabled local group | Monitoring privilege-related changes |
| 4769 | Kerberos service ticket requested | Investigating Kerberos activity |
| 1102 | Audit log cleared | Detecting possible defense evasion |
| 4104 | PowerShell script block logging | Investigating PowerShell execution |

These events are useful investigation artifacts, but their presence alone does not always confirm malicious activity. Analysts must correlate them with timestamps, account names, source addresses, process activity, and other available telemetry.

## 4. Endpoint Visibility with Sysmon

Sysmon provided additional endpoint telemetry to support investigation.

Key takeaways:

- Reviewing process-related activity.
- Investigating suspicious PowerShell execution.
- Understanding the value of process and file activity records.
- Using endpoint telemetry alongside Windows Security logs.

Combining multiple event sources can provide a more complete picture of activity on a Windows endpoint.

## 5. Centralized Monitoring with Wazuh

Wazuh served as the central monitoring platform in the lab.

Practical experience included:

- Receiving security events from monitored systems.
- Reviewing alerts through the Wazuh Dashboard.
- Investigating event details and timestamps.
- Monitoring Windows Security and Sysmon telemetry.
- Reviewing network-related detection alerts integrated into the monitoring environment.
- Exploring automated response through Wazuh Active Response.

## 6. Incident Detection & Investigation

The attack simulations demonstrated the importance of investigating activity across different sources instead of relying on a single alert.

Examples:

- **Brute Force:** Reviewing repeated authentication failures and identifying the targeted account and source.
- **Kerberoasting:** Investigating Kerberos service-ticket request activity.
- **Lateral Movement:** Reviewing successful remote logons and their context.
- **PowerShell Execution:** Examining script-block logging and related endpoint activity.
- **Scheduled Task Persistence:** Investigating task creation events.
- **Event Log Clearing:** Identifying attempts to remove audit evidence.
- **Account Creation:** Correlating account creation with local group membership changes.

## 7. MITRE ATT&CK Knowledge

The scenarios were mapped to relevant MITRE ATT&CK techniques to organize the simulated activities and connect them to recognized adversary behaviors.

The covered areas included:

- Reconnaissance
- Credential Access
- Lateral Movement
- Defense Evasion
- Persistence

This mapping helped provide a structured way to describe attack behavior and organize detection scenarios.

## 8. Key Takeaways

Throughout this project, I gained practical experience in:

- Building and operating a multi-machine SOC home lab.
- Simulating common attack techniques in an isolated environment.
- Monitoring network traffic using Suricata.
- Collecting and investigating Windows security events.
- Working with Sysmon telemetry.
- Centralizing security monitoring with Wazuh.
- Understanding event correlation and investigation context.
- Exploring automated response to suspicious activity.
- Mapping simulated attack scenarios to MITRE ATT&CK.

## 9. Final Notes

This project represents a hands-on learning environment focused on Blue Team operations, security monitoring, attack detection, and incident investigation.

All attack simulations were performed within an isolated virtual lab environment for educational and defensive security purposes.
