# SOC Home Lab Architecture

## 1. Environment Overview

The SOC home lab consists of three virtual machines operating within an isolated internal network.

Each machine has a specific role in the attack simulation and security monitoring process.

## 2. Lab Components

### 1. Kali Linux – Attacker Machine

**Role:** Attack Simulation

Used to simulate adversary techniques against the target environment.

Tools:
- Nmap
- Hydra
- Impacket
- Evil-WinRM

### 2. Windows Server 2019 – Target Machine

**Role:** Active Directory Domain Controller

Configured to provide an enterprise-like Windows environment for testing security monitoring and attack detection.

Security Components:
- Active Directory Domain Services
- Sysmon
- Advanced Audit Policies
- Windows Security Event Logging
- PowerShell Script Block Logging
- ## Wazuh Agent

Wazuh Agent is installed and connected to the Wazuh Manager,
forwarding Windows Security Events and Sysmon telemetry
for centralized monitoring and investigation.

### 3. Ubuntu Server 22.04 – SOC Monitoring Machine

**Role:** Centralized Security Monitoring

Hosts the security monitoring and detection infrastructure.

Components:
- Wazuh Manager
- Wazuh Dashboard
- Suricata IDS
- auditd
- iptables
- ### Wazuh Manager

Receives and analyzes security events forwarded by the
Windows Server Wazuh Agent and displays generated alerts
through the Wazuh Dashboard.

## 3. Network Architecture

All three virtual machines are connected through an isolated internal virtual network.

This setup allows controlled attack simulation while keeping the lab separated from external networks.

### Environment Communication

- Kali Linux generates attack traffic targeting the lab machines.
- Windows Server generates security events related to authentication, system activity, and Active Directory operations.
- Suricata monitors network traffic for suspicious patterns.
- Wazuh provides centralized security event monitoring and alert investigation.
- Ubuntu hosts the monitoring and response components.

## 4. Monitoring Strategy

The environment focuses on three main detection layers:

| Detection Layer | Technology | Purpose |
|---|---|---|
| Network Monitoring | Suricata | Detect suspicious network activity |
| Endpoint Monitoring | Sysmon | Monitor Windows system activity |
| Security Event Monitoring | Windows Auditing | Track authentication and administrative events |
| Linux Auditing | auditd | Monitor Linux system activity |
| Centralized Monitoring | Wazuh | Analyze and investigate security alerts |

## 5. Lab Objectives

- Simulate attacks in a controlled environment.
- Monitor network and endpoint activities.
- Analyze security events generated during attacks.
- Investigate alerts through the Wazuh Dashboard.
- Understand how multiple detection sources contribute to SOC visibility.

## 6. Architecture Evidence

Screenshots and network architecture diagrams will be added here to document the actual lab configuration.
