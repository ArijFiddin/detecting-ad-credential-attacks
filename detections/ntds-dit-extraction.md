# Detection — NTDS.dit Extraction

## MITRE ATT&CK

T1003.003 — OS Credential Dumping: NTDS

## Detection Hypothesis

Detect suspicious attempts to access or copy the Active Directory database,
especially when combined with shadow-copy or administrative utility activity.

## Useful Telemetry

- Process Creation
- File access / creation
- Volume Shadow Copy activity
- Domain Controller security telemetry
- Administrative command execution

## Correlation

```text
Suspicious process
      +
NTDS.dit access/copy
      +
shadow-copy or backup activity
      =
investigate for credential extraction
```

## False Positives

Legitimate backup, recovery, and domain-administration activity may touch
the same resources. Validate the account, host, change window, and expected
administrative workflow.
