# Kerberoasting

## Overview

Kerberoasting is an Active Directory credential-access technique in which an
attacker requests Kerberos service tickets for accounts associated with
Service Principal Names (SPNs) and attempts to crack the ticket material
offline.

From a Blue Team perspective, the important question is:

> What evidence would a domain controller and endpoint generate when this
> activity occurs?

## Analyst Focus

Look for:

- Unusual Kerberos service-ticket requests
- Service accounts that are not normally requested by a user
- A burst of TGS requests in a short period
- Use of RC4 (`0x17`) where it is unusual for the environment
- Suspicious source hosts or accounts
- Related process activity on the requesting host

## Important Telemetry

A key Windows Security event is **Event ID 4769**, which records a Kerberos
service-ticket request.

Useful fields can include:

- Account name
- Service name / SPN
- Client address
- Encryption type
- Timestamp

## Investigation Questions

1. Which account requested the ticket?
2. Which service account / SPN was targeted?
3. Which host generated the request?
4. How many requests occurred within the relevant time window?
5. Is the encryption type expected in this environment?
6. Is the requesting account normally expected to access the service?
7. Are there related endpoint events?

## MITRE ATT&CK

**T1558.003 — Steal or Forge Kerberos Tickets: Kerberoasting**

## Lesson

A single Kerberos ticket request is not automatically malicious. Detection
should consider baselines, volume, encryption type, account behavior, and
source context.
