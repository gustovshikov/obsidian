secure shell

`ssh user@machine` log into machine

- `-p` : specify port : default 22
- `-L` : local tunnel (YOU <-- CLIENT)


### Tunneling

Going to localhost:9000 on your machine, will load site.com traffic
```bash
ssh -L 9000:site.com:80 user@site.com
```

This will forward traffic from blocked firewall on the target machine to your localhost so that you can access the blocked webpage at port 10000
```bash
ssh -L 10000:localhost:10000 <username>@<ip>
```

