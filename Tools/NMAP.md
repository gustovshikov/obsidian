# Network Mapping Tool

# Index
- [Information Gathering](../INE_EJPTv2/Information_Gathering.md#Tools)
- [Footprinting Scanning](../INE_EJPTv2/Footprinting_Scanning.md#Tools)

# Usage: nmap \[Scan Type(s)\] \[Options\] {target specification}
# Examples
- nmap -sn -v 192.168.2.24
- nmap -sn -v -PS21,22,25,80,445,3389,8080 10.4.20.132
- nmap -Pn -PS -v 192.168.8.3
- nmap -Pn -sS -F 10.10.23.4
# Options
### Host discovery
- -sn : no port scan, ping sweep host discovery
	- when scanning directly connected network it will use ARP
		- --send-ip will override
	- -PS : TCP SYN Ping scan, respond with RST
	- -PA : use ACK 
	- -PE : ICMP echo
### Port enumeration
- Default scan without options 
	- does host discovery 
	- SYN scan -sS
	- top 1000 common ports
	- -F : top 100 ports - fast
- -Pn : skip host discovery - windows
- -sS : SYN scan, stealth scan
- -p- : to scan all ports or 
	- -p1-1000 : first 1000
	- -p80,445,3389
- -sU : UDP scan
### Service Enumeration and OS
- -sV : service version detection
- -O : OS detection
- -sC : default scripts
- -A : combines -sV -O -sC
### Additional options
- -v : verbose
- -T0 : 0 - 5 from paranoid to sneaky to insane
- -oN : output to file, several formats available
# Arguments
### Targets
- can specify multiple IPs as multiple arguments
- 10.0.0-255.1-254 or just use CIDR
- -iL : provide IP list by file