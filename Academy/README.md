# Academy

#### IP Address

```bash
EXPORT IP=10.0.2.6
```

Things found on scan:

- port 21 -> FTP
- port 22 -> ssh
- port 80 -> web

## FTP

┌──(mark㉿kali)-[~]
└─$ ftp $IP:
Connected to 10.0.2.6.
220 (vsFTPd 3.0.3)
331 Please specify the password.
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
200 Switching to Binary mode.
ftp> less note.txt
Hello Heath !
Grimmie has setup the test website for the new academy.
I told him not to use the same password everywhere, he will change it ASAP.


I couldn't create a user via the admin panel, so instead I inserted directly int
o the database with the following command:

INSERT INTO `students` (`StudentRegno`, `studentPhoto`, `password`, `studentName
`, `pincode`, `session`, `department`, `semester`, `cgpa`, `creationdate`, `upda
tionDate`) VALUES
('10201321', '', 'cd73502828457d15655bbd7a63fb0bc8', 'Rum Ham', '777777', '', ''
, '', '7.60', '2021-05-29 14:36:56', '');

The StudentRegno number is what you use for login.


Le me know what you think of this open-source project, it's from 2020 so it shou
ld be secure... right ?
We can always adapt it to our needs.

-jdelta
ftp> 

notes file:

gives SQL data for inserion

StudentRegno:
10201321
password:
cd73502828457d15655bbd7a63fb0bc8
pincode:
777777

## Web

Default apache page

Running gobuster against it

found:
- /academy
    - Student Login page
- /phpmyadmin
    - Default credentials isn't allowed
- 


## hash

cracked the hash using hashcat (found out the hash was MD5)
- password: student -> changed to 'password'


## mysql password: 

- "My_V3ryS3cur3_P4ss"
