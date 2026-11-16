# SOC Home Lab: Attack Simulation, Threat Detection & Incident Response

## 1. Project Overview
This project presents a self-built Security Operations Center (SOC) home lab designed to simulate real-world attack techniques, monitor malicious activities, and investigate security alerts through a centralized SIEM environment.

The lab was built to gain practical, hands-on experience in defensive cybersecurity by simulating different attack scenarios against a controlled Active Directory environment and analyzing how these activities are detected and recorded across multiple security monitoring tools.

Rather than focusing only on theoretical knowledge, the project follows an attack-to-detection approach:

- Simulating realistic attack techniques in an isolated environment.
- Monitoring endpoint, network, and authentication activities.
- Collecting and analyzing security events.
- Investigating generated alerts through Wazuh.
- Understanding detection mechanisms and their relevance to SOC operations. 
- Exploring automated incident response capabilities.

The environment consists of three virtual machines working together:

- **Kali Linux:** Used to simulate attacks and adversary techniques.
- **Windows Server 2019:** Configured as an Active Directory Domain Controller and used as the primary target.
- **Ubuntu Server 22.04:** Hosts the SOC monitoring infrastructure, including Wazuh Manager, Wazuh Dashboard, Suricata, and auditd.

The project covers multiple stages of the attack lifecycle, including reconnaissance, credential access, lateral movement, persistence, and defense evasion.

## 2. Project Objectives

The main objectives of this lab are:

- Build a practical and isolated SOC monitoring environment.
- Understand how different attack techniques generate security events.
- Gain hands-on experience with SIEM monitoring and alert investigation.
- Analyze Windows Security Events and Sysmon telemetry.
- Implement network-based threat detection using Suricata.
- Explore automated incident response using Wazuh Active Response.
- Map simulated attack techniques to the MITRE ATT&CK framework.
- Develop practical investigation and threat detection skills from a Blue Team perspective.

## 3. Lab Architecture

The lab consists of three virtual machines connected through an isolated internal virtual network.

### Attacker Machine
**Operating System:** Kali Linux

Tools:
- Nmap
- Hydra
- Impacket
- Evil-WinRM

### Target Machine
**Operating System:** Windows Server 2019

Configuration:
- Active Directory Domain Services
- Domain Controller configuration
- Sysmon
- Advanced Windows Audit Policies
- Windows Security Event Logging
- PowerShell Script Block Logging

### SOC Monitoring Machine
**Operating System:** Ubuntu Server 22.04

Components:
- Wazuh Manager
- Wazuh Dashboard
- Suricata IDS
- auditd
- iptables (for firewall-based response)

## 4. Security Monitoring & Detection Stack

The lab combines multiple monitoring sources to provide visibility across different layers of the environment.

| Component | Purpose |
|---|---|
| Wazuh | Centralized security monitoring, alerting, and event analysis |
| Suricata | Network traffic inspection and intrusion detection |
| Sysmon | Detailed Windows endpoint activity monitoring |
| Windows Security Auditing | Authentication, account management, and system activity monitoring |
| auditd | Linux system auditing |

## 5. Attack Scenarios

The following attack scenarios were simulated and investigated as part of this project.

| # | Attack Scenario | Detection Focus |
|---|---|---|
| 01 | Reconnaissance – Port Scanning | Network-based detection |
| 02 | SSH Brute Force | Authentication failures and automated response |
| 03 | RDP Brute Force | Windows failed logon events |
| 04 | Kerberoasting | Kerberos service ticket requests |
| 05 | Lateral Movement | Remote authentication through WinRM |
| 06 | Obfuscated PowerShell Execution | Script execution and obfuscation |
| 07 | Persistence via Scheduled Task | Scheduled task creation |
| 08 | Defense Evasion – Clearing Event Logs | Security log tampering |
| 09 | Persistence via Backdoor Account | Account creation and privilege assignment |

Each scenario includes its attack overview, simulation details, relevant security events, Wazuh detection evidence, and technical analysis.

## 6. Investigation Methodology

Each attack scenario follows a structured investigation workflow:

1. **Attack Simulation:** Execute the selected attack technique in the isolated lab.
2. **Event Generation:** Observe the resulting endpoint or network activity.
3. **Detection:** Identify the relevant alerts and security events.
4. **Alert Investigation:** Examine event details, timestamps, rule information, and affected systems.
5. **Analysis:** Understand why the activity is suspicious and how it relates to the attack technique.
6. **Response:** Document the response mechanism where applicable.

## 7. Key Learning Outcomes

Through building and testing this environment, the project provides practical exposure to:

- SIEM monitoring and security alert investigation.
- Network and endpoint threat detection.
- Windows Event Log analysis.
- Active Directory security monitoring.
- MITRE ATT&CK technique mapping.
- Authentication attack detection.
- Persistence and lateral movement investigation.
- Automated incident response concepts.

## 8. Tools & Technologies

**SIEM & Monitoring:** Wazuh, Wazuh Dashboard

**Network Security:** Suricata, Nmap

**Endpoint Monitoring:** Sysmon, Windows Security Auditing, auditd

**Attack Simulation:** Kali Linux, Hydra, Impacket, Evil-WinRM

**Operating Systems:** Windows Server 2019, Ubuntu Server 22.04, Kali Linux

**Framework:** MITRE ATT&CK

## 9. Disclaimer

This project was developed exclusively for educational and defensive cybersecurity purposes.

All attack simulations were performed within an isolated virtual lab environment under controlled conditions. No external systems or unauthorized networks were targeted.

Sensitive information, credentials, and identifying network details should be excluded or redacted from publicly shared evidence.
