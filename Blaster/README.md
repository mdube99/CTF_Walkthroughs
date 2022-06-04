[+] Blaster

#### IP Address

```bash
EXPORT IP=10.10.250.18
```

## Nmap

- 80
    - IIS - 10.0
- 3389
    - RDP
    - Target_Name: RETROWEB

## Directories on port 80

Found using ffuf

- /retro

When browsing /retro, found the username "Wade"

While browsing around on the site, I checked the "comments RSS" feed that contained what I believe is a password or user:

parzival

I was able to RDP into the exam using (wade/parzival) and open the user.txt


## Moving files to box

Had a ton of fun moving stuff to box, as certutil was being blocked by AV. Ended up having to use impacket-SMBserver

found that PowerUp.ps1 was blocked by AV, ended up having to put winPEAS

## WinPEAS

While I did not find anything super fun with winPEAS, I looked around the box and found "hhupd" on the desktop

After some googling it seems "hhupd" is commonly used for CVE-2019-1388. Ended up rooting the box with this exploit.

## Trying to setup persistence

Going to metasploit > exploit/multi/script/web_delivery, using PSH as my target

I had some trouble copying and pasting the powershell code, so i put it in a file and copied it over via SMB like i had before.

From here, this got me my meterpreter shell. Establishing persistence is as easy as:

```
run persistence -x
```

where -x -> is on system boot.
