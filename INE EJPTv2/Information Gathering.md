
# INDEX
1. [Intro](#Intro)
2. [Passive Gathering](#Passive-Gathering)
3. [Active Gathering](#Active-Gathering)


## #Intro
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

# #Passive-Gathering

## website Recon & Footprinting

### Tools
##### Terminal
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
### Website scouring
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


# #Active-Gathering

