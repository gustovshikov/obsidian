# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)

# #Overview 
FTP - File Transfer Protocol

file sharing protocol used by different services

## #Ports
- 21 : Win/Lin : Main port for access

## Usage
`ftp 192.156.2.3`
- anonymous login
	- user: anonymous
	- pass: null : just hit enter

## Related Services
vsftp
SFTP
ProFTPD

# #Tools
## #hydra
[hydra](../Tools/Hydra.md)
dictionary attack with *userlist* and *passlist*
- -t : threads
- -L : user File
- -P : pass File
```bash
hydra -L /usr/share/metasploit-framework/data/wordlist/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.168.24.3 -t 4 ftp
```



## #nmap
[nmap](../Tools/NMAP.md)
scripts
```bash
nmap 192.168.24.3 --script ftp-brute --script-args userdb=/root/users -p 21
```
- --script
	- ftp-brute
		- `--sript-args userdb=/userlist.txt`