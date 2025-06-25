# Virtual Machine Configuration

This lab is built using VirtualBox on a host system with 8 GB RAM and 50 GB free disk space.

## 1. Windows Server 2022 (Domain Controller)
- Base OS: Windows Server 2022 (Evaluation)
- RAM: 2 GB
- Disk: 50 GB (VDI, dynamically allocated)
- Network Adapter: Internal Network (`LabNet`)
- Domain: `redblue.lab`
- Hostname: `WIN-DC01`

## 2. Windows 10 Enterprise
- Base OS: Windows 10 Enterprise (Evaluation)
- RAM: 2 GB
- Disk: 40 GB (VDI)
- Network Adapter: Internal Network (`LabNet`)
- Hostname: `WIN10-CLIENT`
- Joined to domain: 

## 3. Kali Linux
- Base OS: Kali Linux Rolling (latest ISO)
- RAM: 2 GB
- Disk: 30 GB (VDI)
- Network Adapter: Internal Network (`LabNet`)
- Hostname: `kali`
