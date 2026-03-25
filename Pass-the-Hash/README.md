## 🔴 Attack 2 — Pass-the-Hash (PtH)

**MITRE ATT&CK:** T1550.002  
**Event ID:** 4624 (Logon Type 9) + Sysmon EventID 1  
**Severity:** Critical  
**Tools Used:** Mimikatz, PsExec, Secretsdump

### Attack Overview

Pass-the-Hash allows an attacker to authenticate using an NTLM hash instead of the plaintext password. By extracting hashes from memory or SAM database, attackers can move laterally across the network without needing the actual password.

### Attack Timeline

| Timestamp | Source | Event | Significance |
|---|---|---|---|
| 2026-03-25 16:04:55 | Security Log — Win10 | EventID 4624 — Type 9 | PtH initiated via seclogo process (Mimikatz).|
| 2026-03-25 16:04:55 |Sysmon EventID 1 | powershell.exe launched | Malicious Process Execution: Started by Mimikatz for control.
| 2026-03-25 16:05:10 | Security Log — Target | EventID 4624 — Type 3 | Successful Lateral Movement to administrative shares. |


### Indicators of Compromise (IOCs)

- Logon Type 9 (New Credentials) without interactive logon
- seclogo or NtLmSsp as logon process
- Unusual source IPs authenticating with domain accounts
- Rapid succession of logon events across multiple systems
- Parent process: seclogo spawning cmd.exe or PowerShell

### Response Actions

- **IMMEDIATE:** Isolate affected machine from network
- Terminate all active sessions for compromised account
- Rotate NTLM hashes for all privileged accounts
- Force password reset for compromised user
- Review all logon events for that account in last 24 hours
- Check for lateral movement to other systems
- Escalate to Incident Response Team — CRITICAL

---
