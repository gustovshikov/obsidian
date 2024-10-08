# Domains

1. [**🛠️ Security Fundamentals**](#Security-Fundamentals)
2. [**🎣 Phishing Analysis**](#Phishing-Analysis)
	1. Types
	2. Tactics
3. [**🧠 Threat Intelligence**](#Threat-Intelligence)
4. [**🕵️ Digital Forensics**](#Digital-Forensics)
5. [**📊 Security Information and Event Management**](#Security-Information-and-Event-Management)
6. [**⏱️ Incident Response**](#Incident-Response)

---

# Security-Fundamentals

1. Physical Security
	1. Access Controls
	2. Monitoring Controls
	3. Deterrents
2. Endpoint security
	1. Host Intrusion Detection
	2. Host Intrusion Prevention
	3. Anti-Virus
	4. Log Monitoring
	5. Endpoint Detection and Response
	6. Vulnerability Scanning
	7. Compliance Scanning
3. Email Security
	1. Spam Filter
	2. Data Loss Prevention
	3. Email Scanning
	4. Security Awareness Training
4. Network Security
	1. Network Intrusion Detection
	2. Network Intrusion Prevention
	3. Firewalls
	4. Log Monitoring
	5. Network Access Control
5. AAA Control Methods
	1. Authentication
	2. Authorization
	3. Accountability

---

#  Phishing-Analysis

## Types
- Recon Emails
	- Spam
		- check if email is valid, error messages
	- Social Engineering
		- Try to get a response
		- impersonation
	- Tracking pixel
		- embedded code that will reach out to a server
		- gather data
			- OS and client information
			- time to read/open
			- ip address
- Credential Harvester
	- Impersonate legit website login pages
	- gathers username/password
- Social Engineering
	- checks for response
	- impersonation to get money etc...
	- gathers information
- Vishing and Smishing
	- Vishing - voice phishing
		- voice call impersonation
		- trys to get money/information
	- Smishing - SMS phishing
		- text message impersonation
		- trys to get money/information
- Whaling
	- targeted phishing attack on important personnel
	- CEO, CFO, CTO, etc...
- Malicous File
	- Office Macros
	- Hosted Malware download
		- can use compromised domain
- Spam
	- normal non-malicious junk email
## Tactics
- Spear Phishing
	- Targeted to a specific user
	- Gathers information on target to be more convincing 
- Impersonation
	- acts/pretends to be another person
- Typosquatting and Homographs
	- Typosquatting
		- impersonating a legit site with minor typo differences
		- IE. I replaced with l, missing char or extra char
	- Homographs
		- uses different char encoding that looks identical to the eye
		- Latin “o” and the Cyrillic “o”
- Sender Spoofing
	- spoof from field in email header
- Hyperlinks
	- embedded malicious links
- Business Email Compromise
## Investigating
- Artifacts
	- Email Info
		- sending address
		- subject line
		- recipient address
		- server ip & reverse DNS
		- Reply-To adress
		- date & time
	- File Info
		- name
		- hash
	- Web Info
		- urls
		- root domains
## Defensive
- Security Technology
	- SPF (sender policy framework)
		- type of DNS TXT record, shows allowed domains
	- DKIM (domain keys identified mail)
		- hash check for integrity of email
	- DMARC (domain-based message authentication, reporting & conformance)
		- builds on SPF & DKIM, allows to specify what happens when checks are failed.
- Spam Filter
	- content
	- rule-based
	- Bayesian
	- attachment
	- sandboxing
- Blocking Artifacts
	- Email sender
	- Sender domain
	- sender server ip
	- subject line
- Blocking File Artifacts
	- hashes
	- names
## Report Writing
- Artifacts collected
	- Sanitize artifacts
- Tools used and results
- Defensive measures taken
## Tools
- URL2PNG
- URLScan
- VirusTotal
- ThreatFeeds
- Talos File Reputation
- Hybrid Analysis
- PhishTool

---

# Threat-Intelligence
“threat intelligence is information that an organization uses to understand the threats that are currently targeting them, or could target them in the future”

## Types of Intelligence
- SIGINT
	- Signal intelligence
	- COMINT - communication intel
	- ELINT - electronic intel
- OSINT
	- Open-source intel
- HUMINT
	- Human intel
- GEOINT
	- geospatial intel
## Types of Threat Intelligence
- Strategic Threat Intel
	- Motives/Goals of group
- Operational Threat Intel
	- TTP - Tactics Techniques and Procedures
- Tactical Threat Intel
	- Technical in nature
	- IOC's
## Threat Actors
- Common Threat Agents
	- Cyber Criminals
	- Nation-States
	- Hacktivists
	- Insider Threat
- Actor Motivation
	- Financial
	- Political
	- Social
	- Unknown
- APT
	- Advanced Persistent Threats
	- Usualy backed by nation states
- TTP
	- Tool, Techniques, and Procedures
## Operational Threat Intel
- Precursors
	- port scanning & fingerprinting services
	- Social Engineering
	- OSINT sources and messaging
- IOC Formating
	- STIX - Structured Threat Information eXpression
	- TAXII - Trusted Automated eXchange of Intelligence Information
- MITRE’s Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK)
- The Cyber Kill Chain (CKC)
	- developed by Lockheed Martin
- pyramid of pain
	- From top to bottom.
```
	                    - TTPs
	                - Tools -----
	            - Network/Host Artifacts
	        - Domain Names ---------------
	    - Ip Adress --------------------------
	- Hash value ---------------------------------
```

---

# Digital-Forensics


---

# Security-Information-and-Event-Management


---

# Incident-Response


