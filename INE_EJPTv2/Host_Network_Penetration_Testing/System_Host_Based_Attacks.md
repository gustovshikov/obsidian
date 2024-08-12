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

### [IIS WebDav](../../Services/IIS-WebDav.md)
### [SMB with PsExec](../../Services/SMB.md#PsExec)


---
## Linux Attacks
