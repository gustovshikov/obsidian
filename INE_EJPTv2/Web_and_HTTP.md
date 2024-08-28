# Overview

## Topics Covered
Introduction To Web Application Security Testing
Common Web Application Threats
Web Application Architecture
Web Application Technologies
HTTP Protocol Fundamentals
HTTP Requests & Responses
HTTPS

---

# Common Web Application Threats
- Cross-Site Scripting (XSS)
- SQL Injection (SQLi)
- Cross-Site Request Forgery (CSRF)
- Security Misconfigurations
- Sensitive Data Exposure
- Brute-Force and Credential Stuffing Attacks
- File Upload Vulnerabilities
- Denial-of-Service (Dos) and DDOS
- Server-Side Request Forgery (SSRF)
- Inadequate Controls
- Using Components with Known Vulnerabilities
- Broken Access Control

# Tools
- Burp Suite
- OWASP ZAP

---

# Web Application Technologies
- Clientside
	- HTML
	- CSS
	- Javascript
	- Cookies and local storage
		- JWT
- Server Side
	- Languages
		- PHP
		- Python
		- Java
		- Ruby
		- etc...
	- WebServer
		- Nginx
		- Apache
		- IIS
		- Node
		- Flask
	- Application Server
		- Code of the app
	- API
		- Restful (REST)
			- CRUD
		- SOAP - Simple Object Access Protocol
		- JSON
		- XML
	- Database
		- PostgreSql
		- MySql
		- etc...

---

# HTTP

## Request Components
1. Line
	1. HTTP method
		- GET
		- POST
		- PUT
		- DELETE
	2. URL (Uniform Resource Locator)
	3. HTTP version
2. Headers
	1. User-Agent : browser information
	2. Host : hostname of server
	3. Accept : media types client can handle eg HTML, JSON
	4. Authorization : credentials
	5. Cookie : client side cookie data
3. Body : Optional Data used in POST / PUT
	1. Data typically in JSON

### Example
```http
GET / HTTP/1.1
Host: www.google.com
User_Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:36.0) Gecko/20100101 Firefox/36.0
Accept: text/html,application/xhtml+xml
Accept-Encoding: gzip, deflate
Connection: keep-alive
```

## Response Components
1. Response Headers
	1. Content-Type : media type (text/html, application/json)
	2. Content-Length : size of the response body in bytes
	3. Set-Cookie : used to set cookies
	4. Cache-Control : directives for caching behavior
2. Body : Optional
	1. content of response such as html

### Example
```http
HTTP/1.1 200 OK
Date: Fri, 13 Mar 2015 11:26:05 GMT
Cache-Control: private, max-age=0
Content-Type: text/html; charset-UTF-8
Content-Encoding: gzip
Server: gws
Content-Length: 258

<!doctype html><html><h1>Page Content</h1></html>
```

