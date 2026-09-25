# Detection — Kerberoasting

## MITRE ATT&CK

T1558.003 — Kerberoasting

## Primary Telemetry

- Windows Security Event ID 4769
- Sysmon Event ID 1 / 10 when endpoint correlation is available

## Detection Hypothesis

A user account generates an unusual burst of Kerberos TGS requests,
especially for service accounts or SPNs that are outside its normal access
pattern.

Additional context can increase confidence:

- RC4 encryption (`0x17`) where uncommon
- Multiple service tickets in a short window
- Unusual source host
- Suspicious endpoint process activity

## Correlation

```text
4769 anomaly
   +
unusual account/service targeting
   +
source-host anomaly
   +
endpoint activity
   =
higher-confidence investigation
```

## False Positives

Potential legitimate causes include:

- Administrative tools
- Service discovery
- Applications requesting many service tickets
- Legacy systems that still use RC4

Tune thresholds and baselines for the environment.
