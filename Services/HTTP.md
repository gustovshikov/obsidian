# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)

---
# Overview

Used to host websites. 

## #Ports
- 80 : HTTP
- 443 : HTTPS
- 8080 : Common Alternative or proxy

## Usage
Use web-browser to access the site via hostname or IP.

## Related Services
- IIS : Windows HTTP Server
- NGINX : Server and Proxy
- Apache : server
- httpd : 

---
# #Tools

## whatweb
grabs information and runs tests
`wahtweb 192.168.32.3`

## http
grabs header information and html of page
`http 10.4.18.3`

## dirb
Will find directories that exists at the website using common built in wordlist using GET.
`dirb http://192.168.32.4`
```bash
dirb http:192.168.32.4 /user/share/metasploit-framework/wordlist/directory.txt
```

## browsh
website enumeration, will render website in ascii
`browsh --startup-url http://10.4.16.3/Default.aspx`
- ctrl-w : to exit

## lynx
similar to browsh, more text oriented

## curl
grabs the page from url

## wget 
grabs files from url

## nmap

```bash
nmap -p80 --script http-enum,http-headers,http-methods,http-webdav-scan --script-args url-path=/ 10.3.24.160
```
`nmap -sV -p80 10.34.5.3`
- --script
	- http-enum
		- will show some dir
	- http-headers
		- grabs http header information, shows service version info
	- http-methods
		- --script-args url-path=/webdav/
	- http-webdav-scan
		- --script-args url-path=/webdav/
	- banner
		- return banner, version info

## msfconsole
Metasploit Framework Console

- use auxiliary/scanner/http/http_version
	- set rhosts 192.15.43.3
	- options
	- run
- use auxiliary/scanner/http/brute_dirs
	- set rhosts 192.165.2.3
	- option
	- run
- use auxiliary/scanner/http/robots_txt
	- set rhosts 192.168.32.3
	- run
- 




