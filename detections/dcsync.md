# Detection — DCSync

## MITRE ATT&CK

T1003.006 — OS Credential Dumping: DCSync

## Primary Telemetry

- Windows Security Event ID 4662
- Directory Replication Service network telemetry where available

## Detection Hypothesis

Detect directory replication activity initiated by an account or source
host that is not expected to perform replication.

## Key Context

- Account
- Source host / source IP
- Replication-related permissions
- Whether the source is a known domain controller
- Time of activity
- Related privileged activity

## Investigation

The main question is:

> Is this replication activity expected for this identity and source host?

Known domain controllers and authorized replication accounts should be
validated against the environment baseline.
