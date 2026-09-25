# NTDS.dit Extraction

## Overview

`NTDS.dit` is the Active Directory database on a domain controller. An
attacker may attempt to access or copy this database to obtain credential
information and other domain data.

## Analyst Focus

Look for:

- Unexpected access to the NTDS database
- Suspicious backup or shadow-copy activity
- Use of administrative utilities to copy or access the database
- File activity associated with the NTDS database
- Suspicious activity originating from a non-standard administrative host

## Important Telemetry

Useful telemetry can include:

- Process creation
- File access / file creation
- Volume Shadow Copy activity
- Administrative utility execution
- Domain Controller security logs

## Investigation Questions

1. Which account accessed or attempted to copy the database?
2. Which process performed the operation?
3. Was a shadow copy created?
4. Was `ntdsutil.exe` or another administrative utility involved?
5. Was the activity performed from an expected administrative system?
6. What happened before and after the database access?

## MITRE ATT&CK

**T1003.003 — OS Credential Dumping: NTDS**

## Lesson

NTDS.dit access should be investigated in the context of the process,
account, host, backup/shadow-copy activity, and administrative baseline.
