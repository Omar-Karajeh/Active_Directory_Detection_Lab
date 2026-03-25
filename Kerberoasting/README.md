## 🔴 Attack 1 — Kerberoasting

**MITRE ATT&CK:** T1558.003  
**Event ID:** 4769 — Kerberos Service Ticket Requested  
**Severity:** High  
**Tools Used:** Rubeus, GetUserSPNs.py

### Attack Overview

Kerberoasting is a technique where an attacker requests Kerberos Service Tickets (TGS) for accounts with Service Principal Names (SPNs) and attempts to crack them offline. The attack targets RC4 encryption (weaker than AES), making tickets vulnerable to brute-force attacks.

### Attack Timeline

| Timestamp | Source | Event | Significance |
|---|---|---|---|
| 2026-03-25 15:02:16 | Security Log — DC | EventID 4769 — TGS requested for SQLSvc | RC4 encryption (0x17) detected — indicator of Kerberoasting |
| 2026-03-25 15:02:16 | Security Log — DC | EventID 4769 — Ticket_Options: 0x40800000 | Matches Rubeus tool signature |
| Offline | Attacker Machine | Offline ticket cracking | Service account password compromised |

### Indicators of Compromise (IOCs)

- Multiple TGS requests for service accounts in short time window
- RC4 encryption type (0x17) used instead of AES
- Unusual source IPs requesting tickets
- High volume of failed service ticket requests

### Response Actions

- Identify compromised service account immediately
- Reset service account password
- Review service account permissions and reduce if necessary
- Check for lateral movement attempts using compromised credentials
- Escalate to Tier 2 Security Team
