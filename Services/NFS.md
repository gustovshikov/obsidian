# Overview

Network Files Share

## Ports
- Port 111 (TCP and UDP) 
- 2049 (TCP and UDP) 

---

# NMAP

```bash
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.10.205.103
```

