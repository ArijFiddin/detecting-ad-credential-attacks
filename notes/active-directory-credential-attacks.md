# Detection Notes

## Detection Objective

Identify suspicious Active Directory authentication activity
that may indicate credential attacks.

## Data Sources

- Windows Security Event Logs
- Domain Controller logs
- Sysmon
- Network telemetry

## Detection Logic

The detection should consider:

1. Repeated authentication attempts
2. Unusual source hosts
3. Suspicious service account activity
4. Authentication involving privileged accounts
5. Authentication patterns inconsistent with normal behavior

## Investigation Questions

When the alert triggers:

- Who is the affected user?
- What system initiated the activity?
- What system was targeted?
- Was authentication successful?
- Is the account privileged?
- Is the source host expected?
- Are there related suspicious processes?
