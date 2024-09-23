
### CMD

Format:
```
\\HOSTIP\SHARENAME
```

List contents of share
```cmd-session
dir \\192.168.220.129\Finance\
```


Maps share to an n: drive
```cmd-session
net use n: \\192.168.220.129\Finance

net use n: \\192.168.220.129\Finance /user:plaintext Password123

```

List mapped share file count
```cmd-session
dir n: /a-d /s /b | find /c ":\"
```

Searching for string in mapped share
```cmd-session
findstr /s /i STRING n:\*.*
```


### PowerShell

List share contents
```powershell-session
Get-ChildItem \\192.168.220.129\Finance\
```
```powershell-session
PS N:\> (Get-ChildItem -File -Recurse | Measure-Object).Count
```

Map share to drive 
```powershell-session
New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem"
```

Passing Credentials to SMB Share
```powershell-session
> $username = 'plaintext'

> $password = 'Password123'

> $secpassword = ConvertTo-SecureString $password -AsPlainText -Force

> $cred = New-Object System.Management.Automation.PSCredential $username, $secpassword

> New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem" -Credential $cred
```

Searching for string in file name
```powershell-session
Get-ChildItem -Recurse -Path N:\ -Include *STRING* -File
```

Search for string in file 
```powershell-session
Get-ChildItem -Recurse -Path N:\ | Select-String "STRING" -List
```
