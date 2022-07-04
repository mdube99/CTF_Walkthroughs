# THM - Ignite

## Rustscan

ports:

- 80
	- apache httpd 2.4.18
	- fuel CMS 1.4
	- robots.txt 1 disallowed entry -> 

## Ffuf

\/assets

## \/fuel

found default credentials to be admin/admin -> was able to login with these, but it was a **giant** honeypot.

I found CVE 2018-16763 and was able to modify it

![[Pasted image 20220703211801.png]]

It initially had a burpsuite addon, I simply just removed this and changed the IP to correspond with the correct one for the box. 

This gave me command execution ability.

From here, I uploaded a PHP reverse shell to get a better shell

![[Pasted image 20220703212134.png]]

I uploaded linpeas to the /tmp directory, and was not able to find anything initially. I saw that it was vulnerable to CVE 2021-4043 (which feels like cheating). I tried finding something else, but I was not finding anything that looked like it would work. I ended up just using this CVE to get root. 

![[Pasted image 20220703212300.png]]

After looking through things more, there was a password shown in the fuel database called "mememe". At first i thought this was an internal password set for accessing the database. Usually this means nothing, but I should have tried it - it was the root password. Another reminder to check everything, no matter what. 