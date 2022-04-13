# dev

#### IP Address

```bash
EXPORT IP=10.0.2.7
```

## Ports

- 22 (SSH) - OpenSSH 7.9p1 Debian 20+deb10u2
- 80 (apache) httpd 2.4.38
- 111 (rpcbind)
- 2049 (nfs_acl 3)
- 8080 (apache)


## Port 80

Bolt installation error, installed in the wrong spot

sub directories found:

/public (301) - nothing here
/src (301) - has customextension.php file that is executable
/app (301) - has other directory (believe the bolt files directory)
/vendor (301) - other directory of files
/extensions (301) - nothing
/server-status (403)


## Port 8080

PHP Version 7.3.27-1~deb10u1

Machine -
    System 	Linux dev 4.19.0-16-amd64 #1 SMP Debian 4.19.181-1 (2021-03-19) x86_64
    Build Date 	Feb 13 2021 16:31:40
    Server API 	Apache 2.0 Handler 

Apache - 
    Apache Version 	Apache/2.4.38 (Debian)
    Apache API Version 	20120211
    Server Administrator 	webmaster@localhost
    Hostname:Port 	127.0.1.1:8080
    User/Group 	www-data(33)/33 
    
mysql - 
    Client API library version 	mysqlnd 5.0.12-dev - 20150407 - $Id: 7cc7cc96e675f6d72e5cf0f267f48e167c2abb23 $ 
    
sqllite3 -
    3.27.2
    
#### Directories on 8080

/dev -> boltwire
/server-status (403)


FOUND -> 


- page that shows the version of boltwire

    Site

    This area gives you access to important site configuration pages. Click links in the side menu to manage different aspects of your site.

    You are currently using Version 6.03 of BoltWire.

From here, found that version 6.03 of boltwire has local file inclusion


#### /etc/passwd

found the user: jeanpaul


## RPC 

had a mountpoint:

/srv/nfs

used 

```bash
mount -t nfs $IP:/srv/nfs
```

once mounted, had a zip file

zip file was encrypted: cracked with johntheripper

#### SSH'd on the system

Can use zip as sudo passwordless


