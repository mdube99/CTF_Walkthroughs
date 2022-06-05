[+] Simple CTF

#### IP Address

```bash
EXPORT IP=10.10.72.245
```

## Nmap scan

Ports open:
- 21 - FTP (vsftpd 3.0.3)
    - logged in as FTP (**ANONYMOUS ALLOWED**)
- 80 - apache httpd 2.4.18
    - robots.txt -> openemr-5_0_1_3
- 2222 - SSH 7.2


## Port 80

default page

robots.txt doesn't say much, but does show:

```
"$Id: robots.txt 3494 2003-03-19 15:37:44Z mike $"
```

Makes me think mike is a possible user (added to initusers.txt)

## Port 21

anonymous access is allowed via FTP, but I can't list the directory. Going to try uploading aspx revshell to see if it's giving access to the apache directory - wouldn't surprise me. 

Unable to upload files via FTP, no joy.

## Port 2222

Not going to take a look at this for a while, as it's SSH

---

After getting stuff from CMS made Simple, I logged in via ssh with the username and password given.

## openemr-5_0_1_3

seems to be an RCE for this, but I cannot view as seen from robots.txt

## Ffuf

- /simple
    - CMS Made simple 

## CMS Made Simple

Once I found this, I went ahead and tried:
- https://www.exploit-db.com/exploits/46635
    - CVE 2019-9053

This got me: 

user: mitch
salt for password: 1dac0d92e9fa6bb2

email found: admin@admin.com
password found: **secret**


reading through the page, the login path is: /simple/admin/login.php


## Rooting the box

After getting initial access with SSH via the username/password found from SQLi, I ran sudo -l to see what I could run as my user. 

vim was one of the programs I was able to run, so I simply just ran "sudo vim", and once inside vim ran: ":sh" and was now root.
