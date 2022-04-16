# Optimum

#### IP Address

```bash
EXPORT IP=10.10.10.8
```

## Nmap Scan

Initial Scan:

port 80,

HttpFileServer httpd2.3

Windows

## First things

```
searchsploit httpfileserver
```

```
┌──(mark㉿kali-vm)-[~/CTF/Optimum]
└─$ searchsploit httpfileserver
--------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                               |  Path
--------------------------------------------------------------------------------------------- ---------------------------------
Rejetto HttpFileServer 2.3.x - Remote Command Execution (3)                                  | windows/webapps/49125.py
--------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results

```

used this exploit, was able to get shell on box as a low level user. 

## Privesc

Initial systeminfo

```
C:\Users\kostas\Desktop>systeminfo
systeminfo

Host Name:                 OPTIMUM
OS Name:                   Microsoft Windows Server 2012 R2 Standard
OS Version:                6.3.9600 N/A Build 9600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Server
OS Build Type:             Multiprocessor Free
Registered Owner:          Windows User
Registered Organization:
Product ID:                00252-70000-00000-AA535
Original Install Date:     18/3/2017, 1:51:36
System Boot Time:          22/4/2022, 11:30:03
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System Type:               x64-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: AMD64 Family 23 Model 1 Stepping 2 AuthenticAMD ~2000 Mhz
BIOS Version:              Phoenix Technologies LTD 6.00, 12/12/2018
Windows Directory:         C:\Windows
System Directory:          C:\Windows\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             el;Greek
Input Locale:              en-us;English (United States)
Time Zone:                 (UTC+02:00) Athens, Bucharest
Total Physical Memory:     4.095 MB
Available Physical Memory: 3.426 MB
Virtual Memory: Max Size:  5.503 MB
Virtual Memory: Available: 4.857 MB
Virtual Memory: In Use:    646 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    HTB
Logon Server:              \\OPTIMUM
Hotfix(s):                 31 Hotfix(s) Installed.
                           [01]: KB2959936
                           [02]: KB2896496
                           [03]: KB2919355
                           [04]: KB2920189
                           [05]: KB2928120
                           [06]: KB2931358
                           [07]: KB2931366
                           [08]: KB2933826
                           [09]: KB2938772
                           [10]: KB2949621
                           [11]: KB2954879
                           [12]: KB2958262
                           [13]: KB2958263
                           [14]: KB2961072
                           [15]: KB2965500
                           [16]: KB2966407
                           [17]: KB2967917
                           [18]: KB2971203
                           [19]: KB2971850
                           [20]: KB2973351
                           [21]: KB2973448
                           [22]: KB2975061
                           [23]: KB2976627
                           [24]: KB2977629
                           [25]: KB2981580
                           [26]: KB2987107
                           [27]: KB2989647
                           [28]: KB2998527
                           [29]: KB3000850
                           [30]: KB3003057
                           [31]: KB3014442
Network Card(s):           1 NIC(s) Installed.
                           [01]: Intel(R) 82574L Gigabit Network Connection
                                 Connection Name: Ethernet0
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.8
Hyper-V Requirements:      A hypervisor has been detected. Features required for Hyper-V will not be displayed.

C:\Users\kostas\Desktop>

```

Used this to find out that the box was x64-based. From here I uploaded winPEAS to see what I could find.

Found an NTLM v2 hash, but of my user - not helpful

winPEAS shows that there are a few unquoted programs, some at startup as well - what i'll start with first.

```
    Folder: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup
    File: C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
   =================================================================================================


    Folder: C:\Users\kostas\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
    FolderPerms: kostas [AllAccess]
    File: C:\Users\kostas\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\desktop.ini (Unquoted and Space detected)
    FilePerms: kostas [AllAccess]
   =================================================================================================


    Folder: C:\Users\kostas\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup
    FolderPerms: kostas [AllAccess]
    File: C:\Users\kostas\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\hfs - Shortcut.lnk (Unquoted and Space detected)
    FilePerms: kostas [AllAccess]
   =================================================================================================


    Folder: C:\windows\tasks
    FolderPerms: Authenticated Users [WriteData/CreateFiles]
   =================================================================================================

```

^ Got honeypotted on this for a bit, decided to try another avenue:

Decided to see if i could find some exploits for the box, found it was vulnerable to ms16_32 (secondary logon handle privesc) - this got me an escalated user.
