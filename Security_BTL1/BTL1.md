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
## Forensics Fundamentals
- Data Representation
	- Binary
	- Base64
	- Hexadecimal
	- Octal
	- ASCII
- File Systems
	- FAT16
	- FAT32
	- NTFS
	- EXT3 / EXT4
- Order of Volatility
	1. Registers & Cache
	2. Memory
	3. Disk
	4. Remote Logging and Monitoring Data
	5. Physical Configuration
		1. Network Topology
		2. Archival Media
- Recovering data
	- Scalpel
- File Analysis
	- exiftool
- Browser Artifacts
- Windows logs
	- `C:\Windows\System32\winevt\Logs`
## Memory Analysis with Volatility
[Volatility Tool Info](../System_Analysis/Volatility.md)

## Disk Analysis with Autopsy
[Autopsy Tool Info](../System_Analysis/Autopsy.md)

## Tools
**Linux**
- Scalpel
- exiftool
- steghide
- nikto
- LiME
- memdump
- **volatility**
**Windows**
- FTK imager
- KAPE: the Kroll Artifact Parser and Extractor
- PECmd.exe
- Windows File Analyzer
- JumpListExploreer

---

# Security-Information-and-Event-Management
## Introduction
- Security Information Management (SIM)
	- Monitoring of events in real-time.
	- Sending and generating alerts and reports.
	- Automatic response to incidents.
	- Correlation of data from multiple sources to improve the quality of the information presented.
	- Translation of event logs from different resources through XML files.
- Security Event Management (SEM)
	- Real-time events monitoring.
	- Obtaining security events in devices and applications within the system.
	- Correlation of events to provide a clear picture of the information system.
	- Analyze logs according to their level of importance.
	- Real-time incident response.
- SIEM
	- Aggregates and analyzes activity from different resources
		- network devices, servers, domain controllers, etc.
	- combination of SIM and SEM
### SIEM Platforms
- Graylog
- Arcsight
- QRadar
- LogRhythm
- Splunk

## Logging
Logs are information generated by devices on application information, system performance, user activities etc.
### Syslog
- Information
	- system logging protocol
	- most networking devices and servers support it
	- UDP 514 - plaintext
	- TCP 514 - plaintext
	- TCP 6514 - Secured/encrypted
- Priority Code
	- (facility code * 8) + Severity value = PRI
#### Facility Code

| Number  | Facility description            |
| ------- | ------------------------------- |
| 0       | Kernel messages                 |
| 1       | User-level messages             |
| 2       | Mail System                     |
| 3       | System Daemons                  |
| 4       | Security/Authorization Messages |
| 5       | Messages generated by syslog    |
| 6       | Line Printer Subsystem          |
| 7       | Network News Subsystem          |
| 8       | UUCP Subsystem                  |
| 9       | Clock Daemon                    |
| 10      | Security/Authorization Messages |
| 11      | FTP Daemon                      |
| 12      | NTP Subsystem                   |
| 13      | Log Audit                       |
| 14      | Log Alert                       |
| 15      | Clock Daemon                    |
| 16 - 23 | Local Use 0 - 7                 |
#### Severity Levels

| Value | Severity      | Keyword | Description            | Condition                                                                              |
| ----- | ------------- | ------- | ---------------------- | -------------------------------------------------------------------------------------- |
| 0     | Emergency     | emerg   | System is unusable     | A panic condition.                                                                     |
| 1     | Alert         | alert   | Action must be taken   | A condition that should be corrected immediately, such as a corrupted system database. |
| 2     | Critical      | crit    | Critical conditions    | Hard device errors.                                                                    |
| 3     | Error         | err     | Error conditions       | Error conditions.                                                                      |
| 4     | Warning       | warning | Warning conditions     | Warning conditions.                                                                    |
| 5     | Notice        | notice  | Normal but significant | Conditions that are not error conditions, but that may require special handling.       |
| 6     | Informational | info    | Informational messages | Informational messages.                                                                |
| 7     | Debug         | debug   | Debug-level messages   | Messages that contain information normally of use only when debugging a program.       |
#### syslog packets
- header
	- Timestamp, Hostname, Application name, Message ID
- Message
	- simple readable text or machine readable
	- contains two labels
		- function - describes the function (facility)
		- Severity level

### Windows Even Logs
Files are in Binary format
- Windows 2000 to WinXP/Windows Server 2003
	- `%WinDir%\system32\Config*.evt`
- Windows Server 2008 to 2019, and Windows Vista to Win10
	- `%WinDir%\system32\WinEVT\Logs*.evtx`
Can use the windows Event Viewer to view and filter the logs.

Common Event IDs

| Event ID | Description                                                       |
| -------- | ----------------------------------------------------------------- |
| 4624     | An account was **SUCCESSFULLY logged on**                         |
| 4625     | An account **FAILED to log on**                                   |
| 4647     | User initiated **logoff**                                         |
| 4648     | A **logon** was attempted **USING EXPLICIT CREDENTIALS**          |
| 4649     | A **replay attack** was **DETECTED**                              |
| 4659     | A **handle to an object** was requested with **INTENT TO DELETE** |
| 4706     | A **new trust** was **CREATED** to a domain                       |
| 4720     | A **user account** was **CREATED**                                |
| 4726     | A **user account** was **DELETED**                                |
| 4732     | A **member was ADDED** to a security-enabled local group          |
| 4672     | Special Logon                                                     |

### Sysmon
Sysmon is a windows system service and device that monitors and logs system activity to the windows even log.

### Sigma signature format
supported platforms
- Splunk
- QRadar
- ArcSight
- Elasticsearch (Elastalert, Query strings, DSL, Watcher, & Kibana)
- Logpoint

## Splunk
[Tool Page](../System_Analysis/Splunk.md)

---

# Incident-Response


