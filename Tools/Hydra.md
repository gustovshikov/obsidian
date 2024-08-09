
# Overview


# Options
- -l/L : username/user File
- -p/P : password/password File

---
## Service Examples

### SMB
### Hydra
`hydra -l admin -P /usr/share/wordlists/rockyou.txt 192.168.33.3 smb`
*lower* case to give string and *upper* case to pass in file
- -l admin : username
- -P /wordlist.txt : pass in wordlist

---
### FTP
dictionary attack with *userlist* and *passlist*
```bash
hydra -L /usr/share/metasploit-framework/data/wordlist/common_users.txt -P /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt 192.168.24.3 ftp
```

---
### SSH
dictionary attack
`hydra -l student -P /usr/share/wordlist/rockyou.txt 192.168.7.3 ssh`

