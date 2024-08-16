Metasploit Framework
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

### FTP
- `search type:auxiliary name:ftp` : find scanner for ftp version
- use module on target to get service version
- `search type:auxiliary name:ftp` : ftp_login for brute forcing
- set user file and pass file
