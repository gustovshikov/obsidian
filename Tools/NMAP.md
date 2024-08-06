
# Found in Locations
[Information Gathering](../INE_EJPTv2/Information_Gathering.md#Tools)
[Footprinting Scanning](../INE_EJPTv2/Footprinting_Scanning.md#Tools)

## Common Flags

	- -sn : no port scan, ping sweep host discovery
	- -Pn : target scan common ports, syn stealth
		- -p- to scan all ports or -p1-1000
		- -F top 100 ports
		- -sU udp scan
	- -sV : service version detection
	- -O : OS detection
	- -sC : default scripts
	- -A : combines -sV -O -sC
	- -T0 : 0 - 5 from paranoid to sneaky to insane
	- -oN : output to file, several formats available