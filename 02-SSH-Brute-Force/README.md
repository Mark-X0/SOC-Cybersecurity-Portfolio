# 02 — SSH Brute Force

## 1. Attack Overview

SSH Brute Force is a password-guessing attack in which an attacker attempts to gain unauthorized access to a remote system by repeatedly trying different password combinations.

In this scenario, Hydra was used from the Kali Linux attacker machine to perform repeated SSH authentication attempts against the target system.

The objective was to evaluate whether repeated failed login attempts could be detected and whether the SOC environment could respond to the suspicious activity.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Credential Access
- **Technique:** T1110 — Brute Force
- **Sub-technique:** T1110.001 — Password Guessing

## 3. Attack Simulation

The attack was performed from Kali Linux using Hydra:

```bash
hydra -l testuser -P rockyou.txt ssh://<TARGET_IP>
```

**Command explanation:**

- `-l testuser`: Specifies the username being targeted.
- `-P rockyou.txt`: Uses a password list for authentication attempts.
- `ssh://<TARGET_IP>`: Specifies the SSH service and target IP address.

Hydra repeatedly attempted to authenticate to the SSH service using the supplied password list.

## 4. Detection & Investigation

The SOC environment monitored authentication activity to identify repeated failed login attempts.

Wazuh collected the relevant authentication events and generated alerts associated with suspicious SSH login activity.

Repeated authentication failures provided an indication of a possible brute-force attempt.

## 5. Active Response

Wazuh Active Response was configured to block the attacker's source IP address using an IP-based firewall rule.

According to the lab configuration, the block was applied for **10 minutes**.

This demonstrated how detection can be followed by an automated response to limit continued unauthorized access attempts.

## 6. Detection Evidence

The investigation included:

- Repeated SSH authentication attempts generated from Kali Linux.
- Authentication failure events collected by the monitoring environment.
- Wazuh alerts associated with the suspicious activity.
- Active Response firewall action blocking the source IP for the configured period.

