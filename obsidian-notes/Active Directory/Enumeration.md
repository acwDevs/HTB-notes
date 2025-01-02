Finding active host within domain
```shell-session
fping -asgq 172.16.5.0/23
```

Finding NULL Sessions

```shell-session
rpcclient -U "" -N 172.16.5.5
```


Password policy
```shell-session
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```

```shell-session
crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol
```

Generating user account list
https://github.com/insidetrust/statistically-likely-usernames

Discovering valid users
```shell-session
enum4linux -U 172.16.5.5  | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
```
```shell-session
crackmapexec smb 172.16.5.5 --users
```
```shell-session
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "
```

Discovering valid users with user list
```shell-session
kerbrute userenum -d inlanefreight.local --dc 172.16.5.5 /opt/jsmith.txt
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

