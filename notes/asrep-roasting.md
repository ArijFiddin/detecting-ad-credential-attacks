# AS-REP Roasting

## Overview

AS-REP Roasting targets Active Directory accounts for which Kerberos
pre-authentication is disabled. The resulting authentication material can be
subjected to offline password cracking.

## Analyst Focus

Look for:

- Requests involving accounts without Kerberos pre-authentication
- Unusual account enumeration or targeting patterns
- Repeated authentication requests
- Unexpected encryption types
- Suspicious source hosts or processes

## Important Telemetry

A key Windows Security event is **Event ID 4768**, which records a Kerberos
authentication-ticket request.

A useful investigation field is the **Pre-Authentication Type**. A value of
`0` can indicate that pre-authentication was not used and should be assessed
against the organization's account configuration and baseline.

## Investigation Questions

1. Which account was requested?
2. Is Kerberos pre-authentication intentionally disabled for that account?
3. Which source host generated the request?
4. Were many accounts queried in a short period?
5. Is the encryption type expected?
6. Is there related process activity on the source host?

## MITRE ATT&CK

**T1558.004 — Steal or Forge Kerberos Tickets: AS-REP Roasting**

## Lesson

The presence of a pre-authentication-disabled account is not itself proof of
an attack. The detection becomes stronger when account targeting, source
context, request volume, and endpoint activity are correlated.
