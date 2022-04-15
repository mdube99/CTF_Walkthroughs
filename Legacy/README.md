# Legacy

#### IP Address

```bash
EXPORT IP=10.10.10.4
```

## Nmap scan

Ports open:

- 139 -> (netbios)
- 445 -> (SMB)
- 3389 -> RDP

NetBIOS name: Legacy\x0Computer name: legacy

Workgroup: HTB\x00

Didn't know exactly where to start, decided to check the smb_version. 

Found out it was Windows XP SP3. Found MS08_067 was an option, found it in metasploit and was able to get a meterpreter shell from it.


## Systeminfo from meterpreter

```
meterpreter > shell
Process 1020 created.
Channel 2 created.
Microsoft Windows XP [Version 5.1.2600]
(C) Copyright 1985-2001 Microsoft Corp.

C:\WINDOWS\system32>systeminfo
systeminfo

Host Name:                 LEGACY
OS Name:                   Microsoft Windows XP Professional
OS Version:                5.1.2600 Service Pack 3 Build 2600
OS Manufacturer:           Microsoft Corporation
OS Configuration:          Standalone Workstation
OS Build Type:             Uniprocessor Free
Registered Owner:          user
Registered Organization:   HTB
Product ID:                55274-643-7213323-23904
Original Install Date:     16/3/2017, 7:32:23
System Up Time:            0 Days, 0 Hours, 19 Minutes, 58 Seconds
System Manufacturer:       VMware, Inc.
System Model:              VMware Virtual Platform
System type:               X86-based PC
Processor(s):              1 Processor(s) Installed.
                           [01]: x86 Family 23 Model 1 Stepping 2 AuthenticAMD ~2000 Mhz
BIOS Version:              INTEL  - 6040000
Windows Directory:         C:\WINDOWS
System Directory:          C:\WINDOWS\system32
Boot Device:               \Device\HarddiskVolume1
System Locale:             en-us;English (United States)
Input Locale:              en-us;English (United States)
Time Zone:                 (GMT+02:00) Athens, Beirut, Istanbul, Minsk
Total Physical Memory:     511 MB
Available Physical Memory: 360 MB
Virtual Memory: Max Size:  2.048 MB
Virtual Memory: Available: 2.005 MB
Virtual Memory: In Use:    43 MB
Page File Location(s):     C:\pagefile.sys
Domain:                    HTB
Logon Server:              N/A
Hotfix(s):                 1 Hotfix(s) Installed.
                           [01]: Q147222
NetWork Card(s):           1 NIC(s) Installed.
                           [01]: VMware Accelerated AMD PCNet Adapter
                                 Connection Name: Local Area Connection
                                 DHCP Enabled:    No
                                 IP address(es)
                                 [01]: 10.10.10.4

C:\WINDOWS\system32>
```

Things to note: x86
OS Version: 5.1.2600
- Q147222 installed (not sure what that means?)


## Next step

From here, i uploaded winPEAS.bat to C:\Windows\Temp - did not work.

Was not able to get winPEASx86.exe to run either. Tried metasploit exploit suggester and crashed the box lol.

Tried these tools, didn't even realize I was already admin on the box. Went to Documents and Settings\Administrator\Desktop and was able to see the root.txt file. 

Realistically I should have checked "getuid" from my meterpreter shell, but i couldn't use whoami from the shell i had. Oh well. Another option would have been uploading whoami.exe from kali.
