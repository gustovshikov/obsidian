# Index
- [Information Gathering](../INE_EJPTv2/Information_Gathering.md#Tools)
- [Footprinting Scanning](../INE_EJPTv2/Footprinting_Scanning.md#Tools)

# Usage: nmap \[Scan Type(s)\] \[Options\] {target specification}

# Options
### Host discovery
- -sn : no port scan, ping sweep host discovery
### Port enumeration
- -Pn : skip host discovery - windows
- -p- : to scan all ports or -p1-1000
- -F : top 100 ports - fast
- -sU : udp scan
### Service Enumeration and OS
- -sV : service version detection
- -O : OS detection
- -sC : default scripts
- -A : combines -sV -O -sC
### Additional options
- -v : verbose
- -T0 : 0 - 5 from paranoid to sneaky to insane
- -oN : output to file, several formats available