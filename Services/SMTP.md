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