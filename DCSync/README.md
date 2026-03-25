## 🔴 Attack 3 — DCSync (Directory Replication)

**MITRE ATT&CK:** T1003.006  
**Event ID:** 4662 — Directory Service Access  
**Severity:** Critical  
**Tools Used:** Mimikatz (dcsync), Secretsdump, Impacket

### Attack Overview

DCSync is a technique where an attacker impersonates a Domain Controller to request credential information from another DC. This allows full extraction of the Active Directory database, including all user hashes and credentials. It's one of the most dangerous AD attacks.

### Attack Timeline

| Timestamp | Source | Event | Significance |
|---|---|---|---|
| 2026-03-25 16:36:45 | Security Log — DC | EventID 4662 — DS-Replication-Get-Changes (GUID: 1131f6aa-9c07-11d1-f79f-00c04fc2dcd2) | Non-DC account requesting AD replication rights |
| 2026-03-25 16:36:45 | Security Log — DC | EventID 4662 — DS-Replication-Get-Changes-All (GUID: 1131f6ad-9c07-11d1-f79f-00c04fc2dcd2) | Full credential dump requested |
| 2026-03-25 16:36:33 | Network Traffic | RPC call to DC (port 135, 49152-65535) | Replication traffic detected |
| 2026-03-25 16:36:46 | Attacker Machine | All AD hashes extracted | Complete compromise of AD environment |

### Indicators of Compromise (IOCs)

- EventID 4662 from non-DC accounts
- DS-Replication-Get-Changes or DS-Replication-Get-Changes-All access
- RPC connections from non-DC systems to DC on high ports
- Account with "Replicating Directory Changes" permissions that shouldn't have it
- Mimikatz-like process names (dcsync, secretsdump, impacket)

### Response Actions

- **IMMEDIATE:** Isolate Domain Controller from network
- **URGENT:** Reset krbtgt password TWICE (2-hour wait between resets)
- Assume ALL AD hashes are compromised — plan for full credential reset
- Enable "Protect Privileged Accounts and Groups" policy
- Audit all accounts with "Replicating Directory Changes" permissions
- Review all domain admin activity in past 30 days
- Consider full AD restore from clean backup
- Escalate to Incident Response + Executive Leadership — CRITICAL BREACH
