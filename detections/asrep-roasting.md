# Detection — AS-REP Roasting

## MITRE ATT&CK

T1558.004 — AS-REP Roasting

## Primary Telemetry

- Windows Security Event ID 4768
- Sysmon Event ID 1 for endpoint context

## Detection Hypothesis

Detect requests associated with accounts that have Kerberos
pre-authentication disabled, especially when the requests form an unusual
enumeration or targeting pattern.

Useful context:

- Pre-Authentication Type = 0
- Request volume
- Source host
- Account baseline
- Encryption type

## Investigation

Validate whether the account is intentionally configured without
pre-authentication before treating the event as malicious.
