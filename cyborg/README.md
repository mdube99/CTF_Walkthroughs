# Cyborg

#### IP Address

```bash
EXPORT IP=10.10.229.237
```

# Nmap scan

Port 22 open (version 7.2p2)

port 80 open (apache default page) 2.4.18

## Directories:

admin (301)
etc (301)

/etc/ ->

had squid directory:
/etc/squid/passwd:


music_archive:$apr1$BpZ.Q.1m$F0qqPwHSOG50URuOVQTTn.
- this is an apach hash. Cracked. **squidward**

/etc/squid/squid.confconf

```bash
    auth_param basic program /usr/lib64/squid/basic_ncsa_auth /etc/squid/passwd
    auth_param basic children 5
    auth_param basic realm Squid Basic Authentication
    auth_param basic credentialsttl 2 hours
    acl auth_users proxy_auth REQUIRED
    http_access allow auth_users
```
# archive.tar

files:

config
- contains ID and Key
data
hints.5
index.5
integrity.5

can't open any of the .5 files -> they are audio files

nonce
readme

## Home directory from music_archive

readme inside stated it was a borg backup. Used the cracked hash from earlier to extract the backup. 
Contained /home/ directory for Alex. 

Inside his documents folder was a note.txt that contained his pw

While on system, uploaded linpeas and found that it was vulnerable to CVE-2021-4034.

Definitely not how they wanted me to privesc, but talk about an easy way to root the box.
