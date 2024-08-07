# Table of Contents
1. [Overview](#Overview)
2. [Tools](#Tools)

# #Overview
After gaining initial access and information you need to gather more in depth information. This involved building a network map and versions of services that are running on devices as well as operating systems. This is valuable to know as the next step will build upon this information to discover vulnerabilities to exploit.
- network mapping
- host discovery
- port scanning
- fingerprinting hosts
- firewall detection and evasion
- saving output from scans!

# #Tools
- [nmap](../Tools/NMAP.md) **<- Go Here**
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
## Types of Scanning
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