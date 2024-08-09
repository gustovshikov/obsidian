# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)
	1. nmap
	2. smbmap
	3. nmblookup
	4.  smbclient
	5. rpcclient
	6. enum4linux
	7. msfconsole

# #Overview 
SMB - Server Message Block

Windows file sharing service
## #Ports
- 135 : Win
- 139 : Win/Lin
- 445 : Win/Lin : Main port for access
## Usage
##### Windows
Manually mounting via *Powershell*.
`net use Z: \\10.4.17.133\C$ password /user:administrator`

##### Linux
configure in */etc/fstab* or use *mount*.
```bash
//10.4.5.123/smb/ /mnt/here cifs \
uid=1000,gid=1000,credentials=/etc/samba/user.conf    0 0
```

## Related Services
- CIFS - Common Internet File Services
	- Generic version used by linux etc... 
- SAMBA
	- open source version of Microsoft active directory

## #Tools
### NMAP
[nmap information](../Tools/NMAP)
#### Scripts
Available in default folder */user/share/nmap/scripts*
**--script**
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
`smbclient -L 192.168.4.3 -U bob`
`smbclient //192.168.4.3/bob -U bob`
- -L : list host
- -N : check for NULL session
	- IPC?
- `smbclient //192.168.4.3/public -N`
	- login and can run commands like *ls*
	- get flag
- -U : username


### rpcclient
can be used to connect to smb
`rpcclient -U "" -N 192.168.2.3`
- -U : user
- -N : no pass
Once logged in
- srvinfo : server info
- enumdomusers : grabs users
- enumdomgroups : graps groups
- lookupnames admin : gets more info on user

### enum4linux
- -o : get OS info
- -U : users information
- -S : shares list
- -G : Groups
- -i : printers 
- -r -u "admin" -p "password1" 192.34.54.3 : return users SID

### msfconsole
Metasploit framework
#### SMB
- use auxiliary/scanner/smb/smb_version
	- options
	- set rhost 192.223.23.3
	- run
- use auxiliary/scanner/smb/smb2
	- options
	- set RHOSTS 192.223.23.3
	- run
- use auxiliary/scanner/smb/smb_enumshares
	- options
	- Set rhosts ipaddr
	- run
- use auxiliart/scanner/smb/smb_login
	- options
	- set rhosts 192.223.23.3
	- set pass_file /usr/share/wordlists/metasploit/unix_passwords.txt
	- set smbuser bob
	- run
- use auxiliary/scanner/smb/pip_auditor
	- options
	- set smbuser admin
	- set smbpass passsword1
	- set rhosts 192.125.42.3
	- run

### Hydra
`hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.33.3 smb`
*lower* case to give string and *upper* case to pass in file
- -l admin : username
- -P /wordlist.txt : pass in wordlist


# Index
1. [Enumeration](../INE_EJPTv2/Assessment_methodologies/Enumeration)