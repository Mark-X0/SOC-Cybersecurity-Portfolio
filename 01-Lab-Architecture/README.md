# SOC Home Lab — Architecture & Environment

## 1. Overview

This project uses a virtualized SOC home lab to simulate attack scenarios and monitor suspicious activities through centralized security monitoring.

The environment consists of three virtual machines connected through an isolated internal network.

The main objective is to generate attack activity from a dedicated attacker machine, monitor the target system and network traffic, and investigate the resulting security events through Wazuh.

## 2. Lab Components

### 2.1 Attacker Machine — Kali Linux

**Role:** Attack Simulation

Kali Linux is used to simulate selected attack techniques against the lab environment.

Tools used include:

- Nmap — Network reconnaissance and port scanning.
- Hydra — Authentication attack simulation.
- Impacket — Active Directory and Kerberos-related testing.
- Evil-WinRM — Windows Remote Management session testing.

### 2.2 Target Machine — Windows Server 2019

**Role:** Target System and Active Directory Environment

Windows Server 2019 was configured as an Active Directory Domain Controller and used as the primary target for the simulated attacks.

Security monitoring components:

- Wazuh Agent — Forwards collected security events to the Wazuh Manager.
- Sysmon — Provides additional endpoint telemetry.
- Windows Advanced Audit Policies — Enables auditing of relevant security activities.
- PowerShell Script Block Logging — Records PowerShell script-block activity.

The monitored activities include authentication attempts, account management, Kerberos requests, scheduled task creation, PowerShell execution, and security log manipulation.

### 2.3 SOC Monitoring Machine — Ubuntu Server 22.04

**Role:** Centralized Security Monitoring

Ubuntu Server hosts the SOC monitoring components.

Tools and services:

- Wazuh Manager — Receives and analyzes security events from monitored endpoints.
- Wazuh Dashboard — Provides a centralized interface for alert review and investigation.
- Suricata IDS — Monitors network traffic and generates intrusion detection alerts.
- auditd — Provides Linux audit monitoring capabilities.

## 3. Network Architecture

All three virtual machines are connected through an isolated internal virtual network.

This allows attack simulations and monitoring activities to take place within a controlled lab environment.

### Communication Flow

```text
             Kali Linux
           (Attacker VM)
                 |
                 | Simulated Attacks
                 v
        Windows Server 2019
       (Active Directory DC)
                 |
        +--------+---------+
        |                  |
        v                  v
   Wazuh Agent           Sysmon
        |
        | Security Events
        v
       Ubuntu Server 22.04
        |
        v
    Wazuh Manager
        |
        v
    Wazuh Dashboard

Network Traffic
        |
        v
     Suricata IDS
        |
        v
  Detection Alert Integration
        |
        v
    Wazuh Monitoring
```

## 4. Monitoring & Telemetry Collection

### Windows Endpoint Monitoring

The Windows Server Wazuh Agent forwards relevant Windows Security events and Sysmon telemetry to the Wazuh Manager.

This provides centralized visibility into endpoint activities.

### Network Monitoring

Suricata monitors network traffic and uses configured detection rules to identify suspicious network behavior, including the simulated port-scanning activity.

Suricata alerts are integrated into the Wazuh monitoring environment for centralized review.

### Linux Monitoring

The Ubuntu monitoring server uses auditd to provide visibility into selected Linux system activities.

## 5. Monitoring Workflow

The lab follows this general workflow:

1. An attack technique is simulated from Kali Linux or on the Windows target, depending on the scenario.
2. The target system or network monitoring component records relevant activity.
3. Wazuh Agent forwards Windows telemetry to the Wazuh Manager.
4. Suricata generates network detection alerts for matching traffic patterns.
5. Wazuh Dashboard is used to review available alerts and event details.
6. The collected evidence is examined to understand the simulated activity.

## 6. Security Monitoring Stack

| Component | Purpose |
|---|---|
| Wazuh Manager | Centralized event analysis and alert management |
| Wazuh Dashboard | Security monitoring and investigation |
| Wazuh Agent | Endpoint event collection and forwarding |
| Suricata IDS | Network intrusion detection |
| Sysmon | Windows endpoint telemetry |
| Windows Audit Policies | Security event generation |
| auditd | Linux audit monitoring |
| Kali Linux | Attack simulation |

## 7. Lab Isolation & Safety

The environment was designed as an isolated virtual lab for educational and defensive security testing.

- Attack simulations were performed against lab systems.
- No production systems were targeted.
- Private IP addresses and sensitive credentials should not be published in project screenshots.
- Testing was conducted for monitoring, detection, and investigation purposes.
