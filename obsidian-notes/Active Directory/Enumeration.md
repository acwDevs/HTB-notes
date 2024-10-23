
Get common user attributes
```powershell-session
Get-ADUser -Identity htb-student
```

Group Details
```powershell-session
Get-ADGroup -Identity "Server Operators" -Properties *
```

Current User Privileges
```powershell-session
whoami /priv
```


