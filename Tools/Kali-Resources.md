# Default locations

## Wordlists

users
- /usr/share/metasploit-framework/data/wordlist/common_users.txt
- /usr/share/wordlists/metasploit/unix_users.txt
pass
- /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt
- /usr/share/metasploit-framework/data/wordlists/common_passwords.txt
- /usr/share/wordlists/rockyout.txt
dir
- /usr/share/wordlists/dirb/big.txt

---

## Kali Built-in

- `gunzip rockyou.txt.gz` 
- `/usr/share/wordlist/rockyou.txt`
- /usr/share/seclists/
	- apt install seclists

### Other useful 
- `/usr/share/webshells/php`
- `/usr/share/windows-binaries/`

# Services Examples
## RDP
- USER : /usr/share/metasploit-framework/data/wordlists/common_users.txt
- PASSWORD : /usr/share/metasploitframework/data/wordlists/unix_passwords.txt

## SSH
- USER : /usr/share/metasploit-framework/data/wordlists/common_users.txt
- PASSWORD : /usr/share/metasploit-framework/data/wordlists/common_passwords.txt

## SMB
- USER : administrator
- PASSWORD : /usr/share/wordlists/metasploit/unix_passwords.txt

- USER : /usr/share/metasploit-framework/data/wordlists/common_users.txt
- PASSWORD : /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

## SAMBA
- USER : root
- PASSWORD : /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

## FTP
- USER : /usr/share/metasploit-framework/data/wordlists/common_users.txt
- Password : /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

**Microsoft IIS FTP**
- User : /usr/share/wordlists/metasploit/unix_users.txt
- Password : /usr/share/wordlists/metasploit/unix_passwords.txt

**VSftpd**
- hydra -L /usr/share/metasploit-framework/data/wordlists/unix_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 10.2.17.5 ftp

## MYSQL
- user : root
- Directory : /usr/share/metasploit-framework/data/wordlists/directory.txt
- Sensitive Files : /usr/share/metasploit-framework/data/wordlists/sensitive_files.txt
- Password : /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt

