Table of contents
1. Overview
2. Servers and Services

---
# Overview

After [Footpringing and Scanning](Footprinting_Scanning) we need to find out specific information on port and services that are running. We want to look at these and enumerate what they do, if they require logins, and what versions of said services are running.

---
# Servers and Services
### Servers
A computer that serves something. Shares information by having open connections which can be exploited.
### Services
The specific applications that are running on a server in order to provide a service. 

# Services

## SMB - Server Message Block
Windows file sharing service
#### Port
- 135 : Win
- 139 : Win/Lin
- 445 : Win/Lin : Main port for access
#### Related Services
- CIFS - Common Internet File Services
	- Generic version used by linux etc... 
- SAMBA
	- open source version of Microsoft active directory
#### Usage
##### Windows
Manually mounting via *Powershell*.
`net use Z: \\10.4.17.133\C$ password /user:administrator`

##### Linux
configure in */etc/fstab* or use *mount*.
```bash
//10.4.5.123/smb/ /mnt/here cifs \
uid=1000,gid=1000,credentials=/etc/samba/user.conf    0 0
```

### NMAP
#### Scripts
Available in default folder */user/share/nmap/scripts*
- smb-os-discovery
	- shows os information like hostname
- smb-protocols
	- find versions of smb that are used
- smb-security-mode
	- can find guest account
- smb-enum-sessions
	- can see logged in users
	- --script-args
		- used to pass in arguments, check script documentation
		- `smbusername=administrator,smbpassword=smbserver_777 10.4.33.42`
- smb-enum-shares
	- finds shares that are accessible 
	- more information available if you login, shows permission
- smb-enum-ls
	- add on to smb-enum-shares
	- will run *ls* in those shares
- smb-enum-users
	- shows users
- smb_server-stats
	- data stats and failed logins
- smb-enum-domains
	- domain information
	- shows if password complexity
- smb-enum-groups
	- user and groups
	- can show other users that might have admin access
- smb-enum-services

### smbmap
can be used to show contents, upload, and download files from SMB service running on a server with a guest or user account.
#### Usage
- If protocol version smbv1 exists you can go with null session attack
	- `smbmap -u guest -p "" -d . -H 10.4.50.3`
- Can use a login that you have
	- -d : To show share directory permission
		- `smbmap -u administrator -p smbserver_777 -d . -H 10.4.32.4`
	- -x : To run a command (RCE)
		- `smbmap -u administrator -p smbserver_777 -H 10.4.32.4 -x 'ipconfig'`
	- -L : List out drives
	- -r C$ : connect to drive and list contents
	- --upload '/hack/backdoor' 'C$\\backdoor' : upload file
	- --download 'C$\\flag.txt' : download file

### nmblookup
- -A : utilizes netbios to connect
### smbclient
`smbclient -L 192.168.4.3 -N`
- -L : list host
- -N : check for NULL session
	- IPC
### rpcclient
can be used to connect to smb
`rpcclient -U "" -N 192.168.2.3`
- -U : user
- -N : no pass
Once logged in
- srvinfo : server info
- enumdomusers : grabs users
- lookupnames admin : gets more info on user

### enum4linux
- -o : get OS info
- -u : users information

### msfconsole
Metasploit framework

#### SMB
- use auxiliary/scanner/smb/smb_version
	- options
	- set rhost 192.223.23.3
	- run
- - use auxiliary/scanner/smb/smb2
	- options
	- set RHOSTS 192.223.23.3
	- run

