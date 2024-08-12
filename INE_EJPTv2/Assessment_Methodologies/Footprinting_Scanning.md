# Table of Contents
1. [Overview](#Overview)
2. [Tools](#Tools)
3. [Host Discovery](#Host_Discovery)
	1. [Types of Scanning](#Types_of_Scanning)
	2. [TCP Three way handshake](#TCP_Three_way_handshake)

# #Overview
After gaining initial access and [Information Gathering](Information_Gathering.md) you need to gather more in depth information. This involved building a network map and versions of services that are running on devices as well as operating systems. This is valuable to know as the next step [(Enumeration)](Enumeration.md) will build upon this information to discover vulnerabilities to exploit.
- network mapping
- host discovery
- port scanning
- fingerprinting hosts
- firewall detection and evasion
- saving output from scans! 

# #Tools
- [nmap](../../Tools/NMAP.md) **<- Go Here**
- wireshark
	- packet capture - pcap
- netstat
	- -antp shows connections open
	- on windows -ano shows connections
- ping
	- ICMP echo 
- fping
	- expends on ping
	- can specify larger number of targets

# Host_Discovery
Mostly just use nmap to gather details on Tagets, Services/Versions, and OSs
## Types_of_Scanning
- ping sweeps
	- ICMP echo requests
- ARP Scanning
	- using ARP to discover hosts
- TCP SYN Ping
	- Half-Open scan
	- start handshake with port then don't respond to SYN-ACK
- UDP Ping
	- send UDP packets
	- can work when ICMP is blocked
- TCP ACK Ping
	- send TCP ACK and listen for reset if port is open
- SYN-ACK Ping
	- send SYN-ACK and listen for reset if port is open

## TCP_Three_way_handshake
### Connection Establishment
1. **Client ---->> SYN** ----->> Server
2. Client <<-- **SYN-ACK <<-- Server**
3. **Client ---->> ACK** ----->> Server
### Connection Termination
1. **Client ---->> FIN** ----->> Server
2. Client <<-- **FIN-ACK <<-- Server**
3. **Client ---->> ACK** ----->> Server