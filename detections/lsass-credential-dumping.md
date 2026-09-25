# Detection — LSASS Credential Dumping

## MITRE ATT&CK

T1003.001 — OS Credential Dumping: LSASS Memory

## Primary Telemetry

- Sysmon Event ID 10 — Process Access
- Sysmon Event ID 1 — Process Creation
- Sysmon Event ID 11 — File Create

## Detection Hypothesis

A non-standard or abnormal process accesses `lsass.exe`, followed by
memory-dump or suspicious file-creation behavior.

## Correlation

```text
Process accesses LSASS
        ↓
Identify process + user + parent
        ↓
Check dump/file creation
        ↓
Check follow-on authentication activity
```

## Tuning

Exclude or separately handle known security products and legitimate
administrative tooling. Detection should be based on behavior and context,
not only process names.
