Finding active host within domain
```shell-session
fping -asgq 172.16.5.0/23
```


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


Generating user account list
https://github.com/insidetrust/statistically-likely-usernames


Finding NULL Sessions

```shell-session
crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol
```

```shell-session
rpcclient -U "" -N 172.16.5.5
```
