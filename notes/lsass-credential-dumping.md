# LSASS Credential Dumping

## Overview

LSASS (Local Security Authority Subsystem Service) can contain credential
material in process memory. An attacker with sufficient access may attempt
to read LSASS memory to obtain credential material.

## Analyst Focus

Look for:

- Unexpected processes accessing `lsass.exe`
- Abnormal process relationships
- Suspicious memory-access behavior
- Memory dump files created shortly after LSASS access
- Related privilege or execution activity

## Important Telemetry

Sysmon **Event ID 10 (Process Access)** can provide visibility into processes
accessing other processes.

Sysmon **Event ID 1 (Process Creation)** and **Event ID 11 (File Create)** can
help correlate the access with the process that performed it and possible
dump-file creation.

## Investigation Questions

1. Which process accessed LSASS?
2. Which user context ran the process?
3. Is the process expected to access LSASS?
4. What was the parent process?
5. Was a memory dump or other suspicious file created?
6. Were there subsequent authentication or lateral-movement events?

## MITRE ATT&CK

**T1003.001 — OS Credential Dumping: LSASS Memory**

## Lesson

LSASS access can have legitimate causes, including security software and
administrative tooling. Detection should therefore use process identity,
signer, parent process, user context, and surrounding events rather than
treating every LSASS access as malicious.
