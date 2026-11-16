# 04 — Kerberoasting

## 1. Attack Overview

Kerberoasting is an Active Directory credential access technique that targets service accounts associated with Service Principal Names (SPNs).

An authenticated domain user can request a Kerberos service ticket (TGS) for an account with a registered SPN. The returned ticket contains encrypted material that can be extracted and subjected to offline password-cracking attempts.

In this lab, Impacket's `GetUserSPNs` tool was used from Kali Linux to identify SPN-associated accounts and request service tickets.

## 2. MITRE ATT&CK Mapping

- **Tactic:** Credential Access
- **Technique:** T1558 — Steal or Forge Kerberos Tickets
- **Sub-technique:** T1558.003 — Kerberoasting

## 3. Attack Simulation

The attack was performed using Impacket:

```bash
impacket-GetUserSPNs <DOMAIN>/<USERNAME>:<PASSWORD> -dc-ip <DC_IP> -request
```

**Command explanation:**

- `<DOMAIN>`: The Active Directory domain name.
- `<USERNAME>`: A valid domain user account.
- `<PASSWORD>`: The account password.
- `-dc-ip <DC_IP>`: Specifies the Domain Controller IP address.
- `-request`: Requests service tickets for accounts with SPNs.

The lab scenario used low-privilege domain credentials to request a TGS ticket for the service account `service.sql`.

The resulting ticket hash was extracted for offline password-cracking analysis.

## 4. Detection & Investigation

Kerberos authentication activity was monitored through Windows Security auditing on the Domain Controller.

The relevant Windows Security event was:

- **Event ID 4769 — A Kerberos service ticket was requested.**

This event records Kerberos service-ticket requests and can provide useful investigation details, including the requesting account, service information, and client address when available.

A single Event ID 4769 does not automatically confirm Kerberoasting. Investigation requires reviewing the event context and identifying unusual service-ticket request patterns.

## 5. Wazuh Alert Evidence

Wazuh centralized the Windows Security events forwarded by the Domain Controller's Wazuh Agent.

The investigation focused on:

- Kerberos service-ticket request activity.
- The requesting domain account.
- The targeted service account or SPN.
- The event timestamp and available source information.

The observed Event ID 4769 was used as supporting evidence during the investigation.

