# Info
secure shell

`ssh user@machine` log into machine
- `-p` : specify port : default 22
- `-L` : local tunnel (YOU <-- CLIENT)

# Port Forwarding

Usage:
```bash
ssh -L [local_port]:[remote_host]:[remote_port] [user]@[ssh_server]
```

This will forward local traffic that is not accessable on localhost:8080 of the target machine back to your port 9090
```bash
ssh -L 9090:localhost:8080 <username>@<ip>
```

# Reverse Port Forwarding:
```bash
ssh -R [remote_port]:[local_host]:[local_port] [username]@[server_ip]
```

To forward traffic from the remote server’s port `9090` to your local machine’s port `8080`, use:
```bash
ssh -R 9090:localhost:8080 <username>@<ip>
```

# SOCKS Proxy

1. **Create an SSH Reverse Tunnel with Dynamic Port Forwarding:**
    
    The key to setting up a proxy server is to use the `-D` option, which specifies dynamic port forwarding. This will create a SOCKS proxy on a specified port on your local machine.
    
    **Command:**
    ```bash
    ssh -D [local_port] [username]@[server_ip]
    ```
    
2. **Example Command:**
    Let’s set up a SOCKS proxy on port `8080` on your local machine that routes traffic through the remote server:
    
    ```bash
    ssh -D 8080 -C -N <username>@<server_ip>
    ```
    
    ### Breakdown:
    
    - **`-D 8080`**: Sets up a SOCKS proxy on your local machine's port `8080`. You can use this port in your browser or any application that supports SOCKS proxies.
    - **`-C`**: Enables compression, which can improve performance for web traffic.
    - **`-N`**: Tells SSH not to execute remote commands, useful when you only want to use the connection for port forwarding.
    - **`<username>@<server_ip>`**: SSH credentials to connect to your remote server.

---

# ssh-keygen

- `-t` : keytype
- `-b` : sets the key size to 4096 bits
- `-C` : optional comment to help identify


```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```