# Jeeves

#### IP Address

```bash
EXPORT IP=10.10.10.63
```

## Nmap scan

- 80 (IIS http 10.0)
- 135 (RPC)
- 445 (workgroup: WORKGROUP)
- 50000 http (Jetty 9.4.z-snapshot)

First thought is to attack Jetty while ffuf enumerates subdirectories for 80/50000

## Ffuf

ffuf found /askjeeves on port 50000

It's jenkins, messed around in the directories and found that you can run scripts from a console. Trying a reverse shell

Was able to get a reverse shell open. 

From here, I went ahead and got a meterpreter shell via 

exploit/multi/script/web_delivery and running a powershell script from my pre-existing session

With a meterpreter session, I used ms16_075 to get root.
