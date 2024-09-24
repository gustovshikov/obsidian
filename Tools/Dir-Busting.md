# feroxbuster

- `-t` 50 : specify 50 threads to use, default is 10
- `-w` : wordlist
- `-u` : url target
- `-x` : extensions to append to words from wordlist

example
```bash
feroxbuster -u http://example.com -w wordlist.txt -o output.txt
```

You can resume from an output file
```bash
feroxbuster -u http://example.com -w wordlist.txt --resume-from /last/processed/path -o resumed_output.txt
```

---

# dirb
Will find directories that exists at the website using common built in wordlist using GET.

`dirb http://192.168.32.4`
```bash
dirb http:192.168.32.4 /user/share/metasploit-framework/wordlist/directory.txt
```

---

# gobuster
similar to dirb but with some more functionality

- `-t` 50 : specify 50 threads to use, default is 10
- `-w` : wordlist
- `-u` : url target
- `-x` : extensions to append to words from wordlist

example
```bash
gobuster dir -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -u 10.10.14.61 
```

specifying extensions
```bash
gobuster dir -u http://10.10.14.61:65524 -x html,txt,php,js,py -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt

```
