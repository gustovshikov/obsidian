# Table of Contents
1. [Overview](#Overview)
2. [Resources](#Resources)
3. [Gathering or Enumeration](#Gathering-Enumeration)
	1. [Tools](#Tools)
	2. [Web Scouring](#Website-Scouring)

## #Overview
- first stage of pen test
- more info the better
- passive and active types
	- passive - without active engaging target
		- through OSINT and online resources
		- IP adresses & DNS information
		- domain names & subdomains
		- email adresses
		- web technologies used
	- active - engaging target directly
		- scanning targets
		- requires authorization
		- open ports
		- internal infrastructure
		- technologies/services

# #Resources
## Practice Sites
- zonetransfer.me
	- can practice dns zone transfers

# #Gathering-Enumeration

## website Recon & Footprinting

### #Tools
##### Terminal
###### Passive
- host
	- DNS lookup utility
	- multiple IP usually indicate proxying services ex. CloudFlare
- whatweb
	- web scanner
- whois
	- WHOIS information query
	- nameservers
- dnsrecon
	- grabs dns records
	- MX, A, AAAA, TXT
- wafw00f
	- detects Web Application Firewalls (WAF)
- sublist3r
	- subdomain information
	- python script
	- uses search engines and other tools to query information
- theharvester
	- OSINT tool for gathering emails, names, subdomains, ip/url
	- helps if you specify engines manually, github has list
###### Active
- dnsenum
	- DNS records
	- can perform zone transfer
	- brute-force
- dig
	- axfr - switches for zonetransfer
- fierce
	- ip & domain scanner
	- brute-force or wordlist
	- zonetransfer
	- quick lightweight
	- great before nmap
- [nmap](../Tools/NMAP.md) 
##### Applications
- HTTrack
	- can be blocked by site
	- uses local hosted webpage
	- downloads entire website
##### Online - resources
- WHOIS
	- query and response tool for IP & domain registration information
- netcraft
	- ip, domain, nameserver
	- SSL/TLS
	- technology used
- dnsdumpster
	- grabs dns record information
	- subdomain A records
- Google Dorking
	- https://www.exploit-db.com/google-hacking-database
	- limit results to site subdomain site:\*.site.com
- Have I been pwned
	- https://haveibeenpwned.com/Passwords
### #Website-Scouring
##### On site
- robots.txt
	- text file information for crawlers
	- disallow and allow sections
- sitemap(s).xml
	- provide search engine sitemap layouts
	- can be helpful for finding directories
	- search engine optimization
##### Browser plugins
- BuiltWith
	- shows what site was built with & what is running
- Wappalyzer - requires account?
	- identifies technologies on website


