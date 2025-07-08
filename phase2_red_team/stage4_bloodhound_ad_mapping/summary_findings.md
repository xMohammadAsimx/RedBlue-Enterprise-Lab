# Stage 4 – BloodHound Active Directory Mapping

---

## Objective

To simulate an adversary's ability to map relationships in an Active Directory (AD) environment using BloodHound.  
The goal was to analyze misconfigurations and identify possible privilege escalation and lateral movement paths.

---

## Tools Used

- **SharpHound.exe** – AD data collection tool (by SpecterOps)
- **BloodHound (Docker GUI)** – Graph-based analysis of AD objects and relationships

---

## Setup Recap

- SharpHound was executed on the Domain Controller (`WIN-8HQD9BBCKGH`) as `Administrator`
- Collected LDAP, session, ACL, group, and trust data
- Output ZIP file (`loot.zip`) was transferred to the Kali machine
- Data uploaded into BloodHound via the web GUI

## Cypher Queries & Results

### 1. Shortest Path to Domain Admin

```cypher
MATCH (n:User), (m:Group {name:"DOMAIN ADMINS@REDBLUE.LAB"}), p = shortestPath((n)-[*..]->(m)) RETURN p
```
See [Shortest_Path_To_Domain_admin.txt](https://github.com/xMohammadAsimx/RedBlue-Enterprise-Lab/blob/mainphase2_red_team/stage4_bloodhound_ad_mapping/screenshot/screenshot/Shortest_Path_To_Domain_admin.txt)

### 2. Kerberoastable Users

```cypher
MATCH (u:User) WHERE u.hasspn = true RETURN u.name
```

- No Kerberoastable accounts found

### 3. DCSync Capable Users

``` cypher
MATCH (n:User)-[:MemberOf*1..]->(g:Group)
WHERE g.objectid =~ "S-1-5-.*" AND n.hasdcsyncrights = true
RETURN n.name
```
- No users with DCSync rights

### 4. Users with Local Admin Access

``` cypher
MATCH (u:User)-[:AdminTo]->(c:Computer) RETURN u.name, c.name
```
- No users with AdminTo relationships

## Observations

- Only one attack path to Domain Admin was identified (via session or group membership)

- No SPNs or DCSync permissions were exposed — a sign of a relatively clean AD

- Despite that, the single path confirms misconfiguration and potential for real-world abuse


