Metasploit Framework
# Table of Contents
1. [Overview](#Overview)
2. [Architecture](#Architecture)
	1. Interfaces
	2. Modules
		1. Meterpreter Payload
	3. Libraries
	4. Diagram
	5. The Penetration Testing Execution Standard (PTES)
3. [Usage](#Usage)
	1. nmap importing or running scan
	2. Auxiliary Modules
	3. [Workflow Examples](#Workflow_Examples)
		1. FTP
		2. SMB
		3. MYSQL
		4. SSH
	4. Show information gathered


---

# Overview

- Interface : Methods of interacting with the MSF
- Module : pieces of code that perform a particular task such as an exploit
- Vulnerability : Weakness or flaw in a system that can be exploited
- Exploit : Piece of code/module that is used to take advantage of a vulnerability
- Payload: piece of code delivered to the target by an expoit with the objective of executing arbitrary commands or providing remote access to attacker.
- Listener : a utility that listens for an incoming connection from a target

---

# Architecture
## Interfaces
- `msfconsole` : All in one interface to the MSF
- `MSFcli` : Command line interface that is useful for scripting, deprecated in 2015 and the functionality migrated into the MSFconsole.
- Armitage : A free java based GUI for the MSF
- Web : web interface

## Modules
A module is a piece of code that can be utilized by the MSF. Libraries facilitate the execution of modules.
- Exploit : A module use to take advantage, usually paired with a payload
- Payload : code delivered to target to take advantage, example is reverse shell
	- Non-staged : payload that is sent to target along with the exploit
	- Staged Payload : first payload contains reverse shell, second part is then downloaded and executed
		- Stagers : used to establish stable connection
		- Stage: payload components that are downloaded
- Encoder : used to encode payloads in order to avoid AV detection
- NOP : used to ensure that payloads sizes are consistent and stability
- Auxiliary : used to perform additional functionality like port scanning and enumeration
### Meterpreter Payload
The meterpreter (meta-interpreter) payload is an advanced multi-functional payload that is executed in memory on the target system. It communicates over a stager socket and provides an attacker with an interactive command interpreter on the target system that facilitates the execution of system commands, file navigation and manipulation key-logging, and etc...

## Libraries
- Rex
- MSF Core
- MSF Base

## Diagram
```
 Tools --------> Rex
                 /\
              MSF Core
                 /\
 Plugins ---> MSF Base <------- Interfaces
                 /\
              Modules
```


---

## The Penetration Testing Execution Standard (PTES)
http://www.pentest-standard.org/index.php/Main_Page

| Penetration Testing Phase           | Metasploit Framework Implementation    |
| ----------------------------------- | -------------------------------------- |
| Information Gathering & Enumeration | Auxiliary Modules                      |
| Vulnerability Scanning              | Auxiliary Modules, Nessus              |
| Exploitation                        | Exploit Modules & Payloads             |
| Post Exploitation                   | Meterpreter                            |
| Privilege Escalation                | Post Exploitation Modules, Meterpreter |
| Maintaining Persistent Access       | Post Exploitation Modules, Persistence |

---

# Usage

## nmap importing or running scan
- `workspace -a Test` : add a new workspace
- `db_import /root/winserver.xml` : import an nmap scan
- `hosts` : show hosts
- `services` : show services detected on the hosts
- `db_nmap -Pn -sV -O` : run and import an nmap scan 

## Auxiliary Modules
- `search portscan` : bring up scanner modules
- `use auxiliary/scanner/portscan/tcp`
- `show options` : check the options
- `set rhosts` : set target
- get access to target 1 and once you have a meterpreter session spawn a shell and `/bin/bash -i` to get bash and then run ifconfig to grab the information of the second network. exit shell
- `run autoroute -s 192.113.124.2` : in meterpreter add route to the network
- drop to background
- load portscan and set rhosts to the 2nd system
- once run, the portscan will be routed through the first machine
- auxiliary/scanner/discovery/udp_sweep : another module to do UDP port sweep

---

## Workflow_Examples

### FTP
1. `search type:auxiliary name:ftp` : find scanner for ftp version
	1. use module on target to get service version
2. `search type:auxiliary name:ftp` : ftp_login for brute forcing
	1. set user file and pass file

### SMB
1. `search type:auxiliary name:smb` : smb_version scanner
	1. use to enumerate smb on target
2. `search type:auxiliary name:smb` : smb_enumusers
	1. `info` give information on the module
3. `search type:auxiliary name:smb` : smb_enumshares
4. smb_login : brute force login
	1. can set user to admin discovered and then try passfile
5. use [smbclient](../Services/SMB.md#smbclient) to login

### WebServer
1. `search type:auxiliary name:http` : http_version
	1. use to find the service version
2. `search type:auxiliary name:http` : http_header
	1. grabs methods and header information
3. `search type:auxiliary name:http` : robots_txt
	1. finds information for the robots file
	2. `curl` a dir to check it out
4. dir_scanner : find directories
	1. `set DICTIONARY` 
	2. `set PATH` 
5. files_dir : find files in directories
6. apache_userdir_enum : look at info
	1. `set USER_FILE /wordlists/common_users.txt`
	2. find valid users then create a custom file to use below with users. This will let you narrow down without having to brute force nonexistent users
7. `search type:auxiliary name:http_login` : brute force login
	1. `set AUTH_URI` : target dir
	2. might need to `unset userpass_file` if providing separately
	3. `set verbose false`
	4. `set USER_FILE /usr/share/metaspolit-framework/data/wordlists/namelist.txt`
	5. `set PASS_FILE /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`

### MYSQL
1. `search type:auxiliary name:mysql` : mysql_version
	1. grab version information
2. `search mysql_login` : brute force login
	1. set userpass_file and user info
3. `search mysql_enum` : needs credentials
	1. set *username* and *password*
4. `search mysql_sql` : needs credentials
	1. allows to execute sql queries
	2. `set SQL "SHOW DATABASES;"`
5. `search mysql_schemadump` : needs credentials
	1. displays schema information

### SSH
1. `serach type:auxiliary name:ssh` : ssh_version
	1. grab version information
2. ssh_enumusers : enumerate users
3. `serach type:auxiliary name:ssh` : ssh_login
	1. brute force password login

### SMTP
1. `serach type:auxiliary name:smtp` : smtp_version
	1. grab version information
2. `serach type:auxiliary name:smtp` : smtp_enum
	1. performs user enumeration


---

## Show information gathered
Depends on workspace and modules ran within
- `hosts`
- `services`
- `loot` : shows stuff like schema gathered
- `creds` : shows credentials
