# RedBlue-Enterprise-Lab

# Red-Blue Enterprise Attack Simulation Lab

## Overview

This project simulates a real-world Active Directory environment and demonstrates both Red Team (attack) and Blue Team (defense) workflows. It showcases practical ethical hacking techniques, domain enumeration, lateral movement, and post-exploitation strategies, built entirely in a virtual lab.

## Lab Setup

* **Domain Controller:** Windows Server 2022 with AD, DNS
* **Client Machine:** Windows 10 Enterprise (joined to domain)
* **Attacker Machine:** Kali Linux
* **Network Type:** VirtualBox Internal Network (`LabNet`)
* **Subnet:** `192.168.56.0/24`

## 🔧 Tools Used

* `nmap` — network scanner
* `enum4linux` — SMB enumeration
* `crackmapexec` — authentication testing and SMB enumeration
* `smbclient` — share listing
* `ldapsearch` — LDAP enumeration
* `BloodHound` — AD relationship graphing
* `Neo4j` — BloodHound backend

---

# Project Structure

```
redblue-enterprise-lab/
├── README.md
├── phase1_lab_setup/
│   ├── topology.png
│   ├── vm_config.md
│   └── network_setup.md
├── phase2_red_team/
│   ├── stage1_recon/
│   │   ├── stage1_hosts.txt
│   │   ├── dc_full_port_scan.txt
│   │   └── win10_full_port_scan.txt
│   ├── stage2_enum/
│   │   ├── stage2_enum4linux.txt
│   │   ├── stage2_smbclient_shares.txt
│   │   ├── stage2_cme.txt
│   │   └── summary_findings.md
│   └── ...
├── phase3_blue_team/              
│   ├── wazuh_setup.md
│   ├── winlogbeat_config.yml
│   └── alert_screenshots/
├── bloodhound/
│   ├── bloodhound_data.zip
│   ├── graph_screenshots/
│   └── notes.md
├── report/
│   └── engagement_report.pdf
└── LICENSE
```

---

## Author's Note

This project is a personal lab created to showcase advanced ethical hacking and Active Directory security skills in a controlled environment. It simulates techniques used by professional Red Teams for training and awareness purposes only.

> **Ethical Disclosure:** All attacks and simulations were performed in a closed virtual lab. Do not attempt any of these techniques on networks you do not own or have permission to test.
