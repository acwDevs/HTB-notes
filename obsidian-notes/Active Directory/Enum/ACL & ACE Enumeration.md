
ACE entry vulnerable permissions
- `ForceChangePassword` abused with `Set-DomainUserPassword`
- `Add Members` abused with `Add-DomainGroupMember`
- `GenericAll` abused with `Set-DomainUserPassword` or `Add-DomainGroupMember`
- `GenericWrite` abused with `Set-DomainObject`
- `WriteOwner` abused with `Set-DomainObjectOwner`
- `WriteDACL` abused with `Add-DomainObjectACL`
- `AllExtendedRights` abused with `Set-DomainUserPassword` or `Add-DomainGroupMember`
- `Addself` abused with `Add-DomainGroupMember`

ObecjtAceType Permission Descriptions
- **GenericAll** - full rights to the object (add users to a group or reset user's password)
    
- **GenericWrite** - update object's attributes (i.e logon script)
    
- **WriteOwner** - change object owner to attacker controlled user take over the object
    
- **WriteDACL** - modify object's ACEs and give attacker full control right over the object
    
- **AllExtendedRights** - ability to add user to a group or reset password
    
- **ForceChangePassword** - ability to change user's password
    
- **Self (Self-Membership)** - ability to add yourself to a group


#### Powerview Commands ####

Always start with this
```powershell-session
Import-Module .\PowerView.ps1
```


Spits out a ton of data on ACL but very time consuming
```powershell-session
Find-InterestingDomainAcl
```

ACL enumeration on a specific user
```powershell-session
$sid = Convert-NameToSid wley
```
```powershell-session
Get-DomainObjectACL -Identity * | ? {$_.SecurityIdentifier -eq $sid} -Verbose
```
Resolve guids for an objectacl
```powershell-session
Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $sid} -Verbose
```

Reverse search using guid
```powershell-session
$guid= "00299570-246d-11d0-a768-00aa006e0529"
```
```powershell-session
Get-ADObject -SearchBase "CN=Extended-Rights,$((Get-ADRootDSE).ConfigurationNamingContext)" -Filter {ObjectClass -like 'ControlAccessRight'} -Properties * |Select Name,DisplayName,DistinguishedName,rightsGuid| ?{$_.rightsGuid -eq $guid} | fl
```

ACL enum for all domain users loop with reference to specified user
```powershell-session
Get-ADUser -Filter * | Select-Object -ExpandProperty SamAccountName > ad_users.txt
```
```powershell-session
foreach($line in [System.IO.File]::ReadLines("C:\Users\htb-student\Desktop\ad_users.txt")) {get-acl  "AD:\$(Get-ADUser $line)" | Select-Object Path -ExpandProperty Access | Where-Object {$_.IdentityReference -match 'INLANEFREIGHT\\wley'}}
```

Query group member info
```powershell-session
Get-DomainGroup -Identity "Help Desk Level 1" | select memberof
```

Query group ACL
```powershell-session
$itgroupsid = Convert-NameToSid "Information Technology"
```
```powershell-session
Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $itgroupsid} -Verbose
```
