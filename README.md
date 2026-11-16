# SOC Home Lab: Attack Simulation, Detection & Investigation

A hands-on Blue Team project focused on simulating common attack techniques, monitoring security events, and investigating detection results using Wazuh, Suricata, Sysmon, and Windows Security Auditing.

## Project Overview

This project demonstrates a self-built SOC home lab designed to practice security monitoring and attack detection in an isolated virtual environment.

The lab consists of three virtual machines:

- **Kali Linux:** Attacker machine used to simulate selected attack techniques.
- **Windows Server 2019:** Active Directory Domain Controller and monitored target.
- **Ubuntu Server 22.04:** SOC monitoring server running Wazuh Manager, Wazuh Dashboard, Suricata IDS, and auditd.

The environment provides visibility across network traffic, Windows endpoint activity, and Active Directory security events.

## Project Objectives

- Build a multi-machine SOC home lab.
- Simulate common attack techniques in a controlled environment.
- Monitor Windows Security events and Sysmon telemetry.
- Detect suspicious network activity using Suricata.
- Centralize security monitoring through Wazuh.
- Investigate alerts and correlate available event details.
- Explore automated response to suspicious authentication activity.
- Map attack scenarios to MITRE ATT&CK.

## Lab Architecture

| Machine | Operating System | Role |
|---|---|---|
| Attacker | Kali Linux | Attack simulation |
| Target | Windows Server 2019 | Active Directory and endpoint monitoring |
| SOC Server | Ubuntu Server 22.04 | Centralized monitoring and detection |

### Monitoring Stack

- Wazuh Manager & Dashboard
- Wazuh Agent
- Suricata IDS
- Sysmon
- Windows Advanced Audit Policies
- PowerShell Script Block Logging
- auditd

**Architecture documentation:** [01-Lab-Architecture](01-Lab-Architecture/README.md)

## Attack Scenarios

The following scenarios were simulated and investigated in the lab.

| # | Attack Scenario | MITRE ATT&CK Technique |
|---|---|---|
| 01 | Reconnaissance — Port Scanning | T1595 — Active Scanning |
| 02 | SSH Brute Force | T1110.001 — Password Guessing |
| 03 | RDP Brute Force | T1110.001 — Password Guessing |
| 04 | Kerberoasting | T1558.003 — Kerberoasting |
| 05 | Lateral Movement via WinRM | T1021.006 — Windows Remote Management |
| 06 | Obfuscated PowerShell Execution | T1027 — Obfuscated Files or Information / T1059.001 — PowerShell |
| 07 | Scheduled Task Persistence | T1053.005 — Scheduled Task |
| 08 | Windows Event Log Clearing | T1070.001 — Clear Windows Event Logs |
| 09 | Backdoor Account Creation | T1136.001 — Create Account: Local Account |

## Attack Documentation & Evidence

Each attack scenario has its own documentation folder containing:

- Attack overview and objective.
- MITRE ATT&CK mapping.
- Simulation commands and explanations.
- Detection and investigation notes.
- Relevant Windows Event IDs, where applicable.
- Screenshots of attack execution and monitoring evidence.


## Investigation Approach

The general investigation workflow used throughout the project:

1. Simulate an attack in the isolated lab.
2. Identify the relevant network or endpoint activity.
3. Review generated security events and telemetry.
4. Investigate the corresponding Wazuh alerts.
5. Examine timestamps, accounts, source addresses, and event details when available.
6. Document the observed activity and supporting evidence.

## Key Learnings

The project provided hands-on experience with:

- Network-based threat detection.
- Windows Security event analysis.
- Sysmon endpoint monitoring.
- Active Directory security monitoring.
- Wazuh alert investigation.
- Suricata IDS rule-based detection.
- Authentication and persistence-related activity.
- MITRE ATT&CK mapping.
- Wazuh Active Response.

## Tools & Technologies

`Wazuh` `Suricata` `Sysmon` `Windows Server 2019` `Ubuntu Server 22.04` `Kali Linux` `Nmap` `Hydra` `Impacket` `Evil-WinRM` `Active Directory` `auditd` `MITRE ATT&CK`

## Disclaimer

This project was developed for educational and defensive security purposes.

All attack simulations were performed within an isolated virtual lab environment. No production systems or unauthorized external targets were involved.

Private IP addresses, passwords, and sensitive information should be excluded from published evidence.

---

**Focus:** Blue Team | SOC Operations | Security Monitoring | Threat Detection | Incident Investigation
