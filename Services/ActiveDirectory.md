
https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/c9113ad0ff443dd0973736552e85aa69.png

https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/d2f78ae2b44ef76453a80144dac86b4e.png


- Password Spraying
	- use same password across all the accounts
- LDAP Pass-back Attacks
	- change printer settings to reach out to your own ldap server to check what credentials are being used.
	- can change the login types to PLAIN,LOGIN to negotiate no encryption
- SMB man in the middle
	- Link-Local Multicast Name Resolution (LLMNR),  NetBIOS Name Service (NBT-NS), and Web Proxy Auto-Discovery (WPAD)
	- intercept request to gran NTLM has to crack directly
	- using `responder` to poison and intercept requests
- MDT and SCCM
	- Microsoft Deployment Toolkit (MDT) 
	- Microsoft's System Center Configuration Manager (SCCM)
- PXE Boot
	- can download a PXE .wim image using tftp and then find credentials coded in the image using powerpxe
- Configuration files
	- Web application config files
	- Service configuration files
	- Registry keys
	- Centrally deployed applications
	- https://github.com/GhostPack/Seatbelt
- Runas : inject credentials 
	- `runas.exe /netonly /user:<domain>\<username> cmd.exe`
- Microsoft Management Console
	- Remote Server Administration Tools' (RSAT) 
- bloodhound ad enumeration
	- https://github.com/BloodHoundAD/BloodHound
- 
