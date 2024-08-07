# Network Mapping Tool

# Table of Contents
1. [Examples](#Examples)
2. [Options](#Options)
	1. Host discovery
	2. Port enumeration
	3. Service and OS Enumeration
	4. Additional options
		3. Timing
		4. Output
3. [Arguments](#Arguments)
4. [Nmap Scripting Engine (NSE)](#Nmap_Scripting_Engine_(NSE))
5. [Firewall avoidance](#Firewall_Avoidance)
6. [Ports](#Ports)
7. [Index](#Index)

# Usage: nmap \[Scan Type(s)\] \[Options\] {target specification}
# #Examples
- nmap -sn -v 192.168.2.24
- nmap -sn -v -PS21,22,25,80,445,3389,8080 10.4.20.132
- nmap -Pn -PS -v 192.168.8.3
- nmap -Pn -sS -F 10.10.23.4
# #Options
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
	- can be used to check if "unfiltered" for Firewalls
- -sA : ACK scan
- -sT : TCP connect scan : send final ACK
- -sU : UDP port scan
- -p- : to scan all ports or 
	- -p1-1000 : first 1000
	- -p80,445,3389
### Service and OS Enumeration
- -sV : service version detection
	- --version-intensity : 0-9 higher is more accurate
- -O : OS detection
	- --osscan-guess : aggressive guessing with percentages
- -sC : default scripts
- -A : combines -sV -O -sC and traceroute
### Additional options
- -v : verbose
##### Timing
- -T0 : Timing Templates
	- 0 - 5 from paranoid, sneaky, polite, default, aggressive, to insane
- --scan-delay/--max-scan-delay \<time\> : Adjust time between packets
- -- host-timeout \<time\> : give up after this time
##### Output
- -oN : normal format
- -oX : XML output : can import to metasploit framework
- -oS : script kiddie
- -oG : grepable format
- -oA : normal, XML, and grepable files
# #Arguments
### Targets
- can specify multiple IPs as multiple arguments
- 10.0.0-255.1-254 or just use CIDR
- -iL : provide IP list by file
# Nmap_Scripting_Engine_(NSE)
Feature that allows you to write automation scripts. Nmap comes with a collection of default scripts.
- /usr/share/nmap/scripts : Default location
-  extension .nse
- written in LUA
- -sC runs default category scripts
	- based on open ports found
	- --script-help=mongodb-databases : information on script
	- --script=mongodb-info : run specific script, category, directory
# Firewall_Avoidance
- -sA : ACK scan : can see if unfiltered vs SYN scan
- --ttl : set time-to-live
- --data-length : Append random data to packets
- -g : source port
- -f : fragment packets
	- --mtu : set MTU for packets
- -D : spoof SRC address such as gateway : only works on same network
- nmap -Pn -sV -p445,3389 -f --data-length 200 -D 10.10.23.1,10.10.23.2 10.4.27.83
# #Ports
### Windows Ports
- 88 : kerberos : TCP/UDP
- 464 : Kerberos : TCP/UDP
- 636 : LDAP over TLS : TCP/UDP
- 3389 : RDP : TCP/UDP
- 137-139 : NetBios : TCP/UDP
### Common Ports
- 22 : SSH
- 23 : telnet
- 25 : SMTP
- 53 : DNS
- 69 : TFTP
- 80 : HTTP
- 110/995 : POP3
- 143/993 : IMAP4
- 443 : HTTPS
### Database
- 3306 : MySQL
- 5432 : PostgreSQL

# #Index
- [Information Gathering](../INE_EJPTv2/Information_Gathering.md#Tools)
- [Footprinting Scanning](../INE_EJPTv2/Footprinting_Scanning.md#Tools)