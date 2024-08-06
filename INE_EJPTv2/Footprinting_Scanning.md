# Table of Contents
1. [Overview](#Overview)
2. [Tools](#Tools)

# #Overview
After gaining initial access you need to gather more in depth information on ports and services that are running. 
- network mapping
- host discovery
- port scanning
- fingerprinting hosts
- firewall detection and evasion
- saving output from scans!

# #Tools
- [nmap](../Tools/NMAP.md)
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
-