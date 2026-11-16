# 01 — Reconnaissance: Port Scanning

## 1. Attack Overview

Reconnaissance is an initial phase of an attack in which an attacker gathers information about a target system before attempting further exploitation.

In this scenario, Nmap was used from the Kali Linux machine to perform a port scan against the Windows Server target and identify exposed network services.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Reconnaissance
- **Technique:** T1595 — Active Scanning

## 3. Attack Simulation

The scan was performed from Kali Linux using Nmap:

```bash
nmap -sS -p- <TARGET_IP>
```

**Command explanation:**
- `-sS`: Performs a TCP SYN scan.
- `-p-`: Scans all TCP ports.
- `<TARGET_IP>`: The IP address of the target Windows Server.

The objective was to identify open ports and discover potentially exposed services.

## 4. Detection & Investigation

Network scanning activity was monitored using Suricata IDS.

A custom threshold-based detection rule was configured to identify suspicious port-scanning behavior.

When the scanning activity was detected, Suricata generated an alert that was forwarded to the Wazuh monitoring environment for centralized visibility and investigation.

## 5. Detection Evidence

The detection was verified through the following evidence:

- Nmap scan activity from the Kali Linux attacker machine.
- Suricata detection alert.
- Corresponding alert visibility in the Wazuh Dashboard.

## 6. Screenshots

### Attack Execution — Kali Linux

_Add Kali Linux screenshot showing the Nmap command and scan results._ 




### Detection Evidence — Wazuh Dashboard

_Add Wazuh screenshot showing the corresponding alert and event details._
