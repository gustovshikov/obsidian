# Table of Contents
1. [Overview](#Overview)
2. [Resources](#Resources)
3. [Gathering or Enumeration](#Gathering-Enumeration)
	1. [Tools](#Tools)
	2. [Web Scouring](#Website-Scouring)

## #Overview
First stage of penetration test. Gather passive knowledge of targets through open source intelligence (OSINT) and queries of public information. Afterwards you move on to actively engaging the targets discovered which leads into [footprinting and scanning](Footprinting_Scanning.md).
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

# Resources
## Practice Sites
- zonetransfer.me
	- can practice dns zone transfers

# Gathering-Enumeration

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
- ffuf
	- brute-force subdomain, CDN blocks this
	- `ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://10.10.190.205 -fs <size>`
	- -fs {size} : replace from the most occurring size when ran without
	- -w : wordlist
	- -H add/edits a header, FUZZ keyword in spot 
	- -u : url
	- -mr : text on page looking for
	- -d : data we are sending
	- -X : request method
- Example
```bash
ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.230.40/customers/signup -mr "username already exists"
```
- W1 and W2 placeholders for wordlists comma separated
- -fc : check for HTTP status code
```bash
ffuf -w users.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.10.230.40/customers/login -fc 200
```

- Discover
	- Passiv or Active
	-  https://github.com/leebaird/discover
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
- [nmap](../../Tools/NMAP.md) 
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
### Website-Scouring
##### On web-site
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
- FoxyProxy


