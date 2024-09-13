# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Vulnerabilities
2. [Tools](#Tools)

---
# Overview
Remote Desktop Protocol is a GUI based remote access protocol develeoped by Microsoft.

Authentication requires a user account and password in clear-text.

## Ports
3389 : TCP

## Usage
`xfreerdp /u:administrator /p:qwertyuiop /v:10.2.24.32:3389`
- freerdp : another client

## Related Services

# Vulnerabilities
## CVE-2019-0708 - BlueKeep
Potentially allow attackers to remotely execute arbitrary code. Takes advantage of a vulnerability in the RDP protocol that allows attackers to gain access to a chunk of kernel memory.
- msfconsole
	- search bluekeep
- !! This can crash the system

---
# Tools

## #msfconsole
- **use auxiliary/scanner/rdp/rdp_scanner**
	- set rport 3333
	- set rhosts 10.2.24.84

## #hydra
Brute force logins with dictionary
```bash
hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt \
-P /usr/share/metasploit-framework/unix_passwords.txt \
rdp://10.2.24.85 -s 3333
```

