# Devel

#### IP Address

```bash
EXPORT IP=10.10.10.5
```


## Initial Nmap scan

ports open:

- 21 (FTP)
    - Windows_NT


- 80 (IIS 7.5)

### FTP

- Anonymous login
    - With write access:
        - Was able to put an aspx reverse shell, load it from web ($IP/aspxreverse.aspx)
        - This got me access


### Initial Access

After getting a revere shell, I was a super low level user. Didn't have wget or curl, so I used certutil to download winPEAS.bat. I had to go to Windows\Temp (going down a couple directories from where i started)

From here, i tried multiple versions of winPEAS unsuccessfully, before I just did the .bat version (initially tried the .exe's)

# Devel

From here, i used the metasploit local exploit suggester, and saw MS010-51 as an option. I found a proof of concept on github, and uploaded it via FTP to the box. Once on the box, I was able to get a reverse shell as an escalated user.
