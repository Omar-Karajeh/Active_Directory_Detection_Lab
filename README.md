# Active Directory Detection Lab

## Overview
Home lab simulating real-world AD attacks detected via Splunk SIEM.

## Environment
- Domain Controller: Windows Server 2022
- Client Machine: Windows 10
- SIEM: Splunk (Sysmon + Windows Security Logs)
- Virtualization: VMware

## Attacks Covered
| Attack | MITRE ID | Event ID | Severity |
|---|---|---|---|
| Kerberoasting | T1558.003 | 4769 | High |
| Pass-the-Hash | T1550.002 | 4624 | Critical |
| DCSync | T1003.006 | 4662 | Critical |

## Detection Queries
Each attack folder contains:
- Splunk SPL query
- Attack description
- IOCs (Indicators of Compromise)
- Recommended response actions
