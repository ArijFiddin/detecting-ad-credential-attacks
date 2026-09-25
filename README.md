# Detecting Active Directory Credential Attacks

A Blue Team learning and detection casebook based on the TryHackMe
**Detecting AD Credential Attacks** room.

The goal of this repository is not to reproduce a walkthrough. It documents
my understanding of Active Directory credential attacks, the telemetry that
can expose them, detection hypotheses, and a SOC-style investigation workflow.

## Attack Coverage

| Technique | MITRE ATT&CK | Focus |
|---|---|---|
| Kerberoasting | T1558.003 | Suspicious Kerberos TGS requests |
| AS-REP Roasting | T1558.004 | Accounts without Kerberos pre-authentication |
| LSASS Credential Dumping | T1003.001 | Suspicious access to LSASS memory |
| DCSync | T1003.006 | Unauthorized directory replication |
| NTDS.dit Extraction | T1003.003 | Access/copy of the AD database |

## Investigation Challenge

The final section combines the individual techniques into a practical
investigation workflow:

```text
Alert
  ↓
Identify affected account / host
  ↓
Validate the relevant Windows telemetry
  ↓
Correlate related events
  ↓
Map behavior to MITRE ATT&CK
  ↓
Assess maliciousness and scope
  ↓
Document findings
```

## Repository Structure

```text
.
├── README.md
├── notes/
│   ├── kerberoasting.md
│   ├── asrep-roasting.md
│   ├── lsass-credential-dumping.md
│   ├── dcsync.md
│   └── ntds-dit-extraction.md
├── detections/
│   ├── kerberoasting.md
│   ├── asrep-roasting.md
│   ├── lsass-credential-dumping.md
│   ├── dcsync.md
│   └── ntds-dit-extraction.md
├── investigation/
│   └── investigation-challenge.md
└── references/
    └── mitre-attack.md
```

## Skills Demonstrated

- Active Directory security monitoring
- Windows Event Log analysis
- Detection engineering
- Threat hunting
- MITRE ATT&CK mapping
- SOC investigation and documentation
- Security telemetry correlation

## Learning Environment

- TryHackMe
- Active Directory / Windows domain environment
- Windows Security Event Logs
- Sysmon concepts
- SIEM and detection engineering concepts

## Disclaimer

This repository contains personal learning notes and defensive security
research. It is intended for authorized educational and security-testing
environments.
