# Active Directory

## Overview

Active Directory (AD) is a directory service commonly used to
manage users, computers, groups, and authentication within a
Windows domain environment.

From a Blue Team perspective, Active Directory is an important
source of security telemetry because authentication and account
activity can provide evidence of suspicious behavior.

## Security Perspective

A SOC analyst should pay attention to:

- Authentication attempts
- Account activity
- Privileged accounts
- Service accounts
- Unusual authentication sources
- Failed authentication attempts
- Successful authentication after multiple failures

## Relevant Telemetry

Potential sources of evidence include:

- Windows Security Event Logs
- Domain Controller logs
- Sysmon
- Network telemetry

## Investigation Questions

When investigating suspicious AD activity:

1. Which account was involved?
2. Which computer initiated the activity?
3. Which computer was targeted?
4. Was authentication successful?
5. Was the account privileged?
6. Were there repeated attempts?
7. Are there related processes or network connections?

## Key Takeaway

Active Directory authentication telemetry can provide valuable
evidence for detecting credential-related attacks.
