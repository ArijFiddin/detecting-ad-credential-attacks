# Kerberoasting Detection

## Overview

Kerberoasting is an Active Directory credential-access technique that targets accounts associated with Service Principal Names (SPNs).

A domain user can request a Kerberos service ticket for an SPN. The ticket can then be obtained and potentially subjected to offline password cracking.

Service accounts can be valuable targets because they may use weak or old passwords and can sometimes have elevated privileges.

---

## How Kerberoasting Works

The basic attack flow is:

Domain User  
→ Requests Kerberos Service Ticket  
→ Domain Controller  
→ Service Ticket  
→ Attacker obtains ticket material  
→ Offline password cracking  
→ Possible service account compromise

The important point for detection is that the Domain Controller generates security telemetry when the service ticket is requested.

---

## Detection Telemetry

### Windows Event ID 4769

**Event ID 4769 — A Kerberos service ticket was requested**

Important fields include:

| Field | Description |
|---|---|
| `Account_Name` | Account requesting the service ticket |
| `Service_Name` | Service/SPN targeted by the request |
| `Ticket_Encryption_Type` | Encryption type used by the ticket |
| `Client_Address` | Source address of the requesting system |

These fields can be used to investigate suspicious Kerberos service-ticket activity.

---

## RC4 as a Detection Signal

One useful indicator is:

```text
Ticket_Encryption_Type = 0x17

0x17 represents RC4-HMAC.

RC4 can be useful as a detection signal when it is unusual in the environment. However, RC4 alone does not prove Kerberoasting because legitimate systems can also generate RC4 Kerberos traffic.

A stronger detection combines:

Event ID 4769
Unusual encryption type
Multiple service accounts being targeted
Short time window
Requesting account
Source IP
Normal behavior/baseline

Splunk Investigation
Identify suspicious RC4 service-ticket requests

index=task2 EventCode=4769 Ticket_Encryption_Type=0x17 Service_Name!="*$" Service_Name!="krbtgt"
| table _time, Account_Name, Service_Name, Ticket_Encryption_Type, Client_Address
| sort _time

Aggregate requests by account and source

index=task2 EventCode=4769 Ticket_Encryption_Type=0x17 Service_Name!="*$" Service_Name!="krbtgt"
| stats dc(Service_Name) as targeted_services count by Account_Name, Client_Address

Investigation Result

| Finding                   | Result        |
| ------------------------- | ------------- |
| Service accounts targeted | 9             |
| Requesting account        | `emma.wilson` |
| Source IP                 | `10.5.90.1`   |

