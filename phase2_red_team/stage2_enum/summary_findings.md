# Stage 2: SMB & Domain Enumeration

This document summarizes the enumeration attempts performed against the domain controller (`192.168.56.101`) during Stage 2 of the red team simulation.

---

## Tools Used

- `enum4linux -a 192.168.56.101`
- `smbclient -L //192.168.56.101 -U '' -N`

---

## Key Observations

### Domain Information (from enum4linux)
- **Domain Name:** `REDBLUE`
- **Domain SID:** `S-1-5-21-1334311049-3276625038-2870192795`
- **Detected as Domain Controller**: Yes
- **Anonymous SMB Session:** Allowed (but restricted)

---

### User Enumeration
- **Attempted Methods:** querydispinfo, enumdomusers, RID cycling
- **Result:** All denied with `NT_STATUS_ACCESS_DENIED`
- **Interpretation:** Domain controller has **restricted anonymous access**, which is a good security practice

---

### Share Enumeration
- **Via enum4linux:**  
  Error: `NT_STATUS_RESOURCE_NAME_NOT_FOUND`
- **Via smbclient:**  
  Could not list shares anonymously
- **Interpretation:** Share listing is **blocked for unauthenticated users**

---

### Password Policy
- `polenum` and `rpcclient` failed to extract policy
- Likely reason: access denied due to null session restrictions

---

### Session-Level Information (NetBIOS / NBT)
- System Name: `WIN-8HQD9BBCKGH`
- Domain: `REDBLUE`
- File Server, Domain Controller, Master Browser flags were active

---

## Analyst Insight

The domain controller (`192.168.56.101`) is configured to **reject most anonymous enumeration attempts** over SMB. This is a secure default configuration on modern Windows Server systems and limits an attacker’s ability to gather information without valid credentials.

However, the system:
- Responds to SMB probes
- Allows null sessions (connects, but with minimal access)

This behavior will guide the next stage, where we will attempt to **authenticate using valid credentials**.

---

## Output Files
- `stage2_enum4linux.txt` – Full enum4linux output
- `stage2_smbclient_shares.txt` – Guest-level share listing attempt

---
