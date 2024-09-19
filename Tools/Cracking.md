## Hash-Types

| Value | Hashing Algorith |
| ----- | ---------------- |
| $1    | MD5              |
| $2    | Blowfish         |
| $5    | SHA-256          |
| $6    | SHA-512          |

## Cracking
- Unshadow file to cleanup "shadow" file for John. Needs `passwd` and `shadow` files
	- `unshadow [path to passwd] [path to shadow]`
- Converting Files to crack
	- zip2john
	- rar2john
	- ssh2john
- John The Ripper
	- `john [options] password-files` : usage
	- `--list=formats` : shows available formats
	- `--format=NT` : specify format/hash type
		- NT
		- sha512crypt
	- `--wordlist=/usr/share/rockyou.txt` : specify wordlist
	- `john --format=sha512crypt --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt`
- Hashcat
	- -m : hash type id found in help menu
		- `hashcat --help | grep -i 512` : look for sah512 or ntlm
	- -a : attack type id found in help menu
	- `hashcat -a 3 -m 1000 hashes.txt /usr/share/wordlists/rockyou.txt`
		- brute force NT hash on *hashes.txt* with wordlist *rockyou.txt*
	- `hashcat -a 3 -m 1800 hashes.txt /usr/share/wordlists/rockyou.txt`

```
Usage: hashcat [options]... hash|hashfile|hccapxfile [dictionary|mask|directory]...

- [ Basic Examples ] -

  Attack-          | Hash- |
  Mode             | Type  | Example command
 ==================+=======+==================================================================
  Wordlist         | $P$   | hashcat -a 0 -m 400 example400.hash example.dict
  Wordlist + Rules | MD5   | hashcat -a 0 -m 0 example0.hash example.dict -r rules/best64.rule
  Brute-Force      | MD5   | hashcat -a 3 -m 0 example0.hash ?a?a?a?a?a?a
  Combinator       | MD5   | hashcat -a 1 -m 0 example0.hash example.dict example.dict
  Association      | $1$   | hashcat -a 9 -m 500 example500.hash 1word.dict -r rules/best64.rule
```
