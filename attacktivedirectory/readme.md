# AttacktiveDirectory

# Nmap scan:


53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-title: IIS Windows Server
|_http-server-header: Microsoft-IIS/10.0
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2022-01-13 18:44:16Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: spookysec.local0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: spookysec.local0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
3389/tcp open  ms-wbt-server Microsoft Terminal Services

**SMB Security Signatures required**

------

This nmap scan showed the domain. Domain: THM-AD

Device name: AttacktiveDirectory


First question from THM was what is the domain name: THM-AD

Second question was what was the TLD: .local

I used enum4linux to enumerate the box

From here, i used kerbrute to enumerate users. 

I was able to get a password hash using the backup account for svc-admin

I used secretsdump on this and dumped all the hashes for the system, from here i just logged on and grabbed what i needed to complete
