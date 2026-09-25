# DCSync

## Overview

DCSync abuses Active Directory replication functionality to obtain credential
information by requesting replication data from a domain controller.

The technique is especially important to a SOC because it can expose
credentials associated with highly privileged or sensitive domain accounts.

## Analyst Focus

Look for:

- Replication activity initiated by unexpected accounts
- Replication requests from non-domain-controller systems
- Unexpected use of replication-related permissions
- Related privileged-account activity
- Correlation with suspicious source hosts

## Important Telemetry

Windows Security **Event ID 4662** can provide visibility into directory
service object-access activity when the appropriate auditing and SACLs are
configured.

Network telemetry around the Directory Replication Service can provide
additional context.

## Investigation Questions

1. Which account initiated the activity?
2. Is that account legitimately allowed to perform replication?
3. Which host generated the request?
4. Is the source a known domain controller?
5. Were sensitive accounts involved?
6. What activity happened immediately before and after the replication event?

## MITRE ATT&CK

**T1003.006 — OS Credential Dumping: DCSync**

## Lesson

A strong DCSync detection combines identity, source-host context, directory
permissions, and replication telemetry. Legitimate replication should be
distinguished from unexpected replication initiated by non-DC systems.
