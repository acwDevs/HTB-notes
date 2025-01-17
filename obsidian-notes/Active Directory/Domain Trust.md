
### Enumeration

Powershell cmdlet
```powershell-session
PS C:\htb> Import-Module activedirectory
PS C:\htb> Get-ADTrust -Filter *
```

Powerview
```powershell-session
Get-DomainTrust
```

Powerview
```powershell-session
Get-DomainTrustMapping
```

Find users in child domain
```powershell-session
Get-DomainUser -Domain LOGISTICS.INLANEFREIGHT.LOCAL | select SamAccountName
```

netdom for domain trust
```cmd-session
netdom query /domain:inlanefreight.local trust
```

netdom query domain controller
```cmd-session
netdom query /domain:inlanefreight.local dc
```

netdom query workstation
```cmd-session
netdom query /domain:inlanefreight.local workstation
```



Trust types
- `Parent-child`: Two or more domains within the same forest. The child domain has a two-way transitive trust with the parent domain, meaning that users in the child domain `corp.inlanefreight.local` could authenticate into the parent domain `inlanefreight.local`, and vice-versa.
- `Cross-link`: A trust between child domains to speed up authentication.
- `External`: A non-transitive trust between two separate domains in separate forests which are not already joined by a forest trust. This type of trust utilizes [SID filtering](https://www.serverbrain.org/active-directory-2008/sid-history-and-sid-filtering.html) or filters out authentication requests (by SID) not from the trusted domain.
- `Tree-root`: A two-way transitive trust between a forest root domain and a new tree root domain. They are created by design when you set up a new tree root domain within a forest.
- `Forest`: A transitive trust between two forest root domains.
- [ESAE](https://docs.microsoft.com/en-us/security/compass/esae-retirement): A bastion forest used to manage Active Directory.

![[trusts-diagram.webp]]