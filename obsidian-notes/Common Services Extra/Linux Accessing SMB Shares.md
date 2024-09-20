
Mounting share to a folder

```shell-session
$ sudo mkdir /mnt/Finance

$ sudo mount -t cifs -o username=plaintext,password=Password123,domain=. //192.168.220.129/Finance /mnt/Finance
```
OR
Using creds file
```shell-session
mount -t cifs //192.168.220.129/Finance /mnt/Finance -o credentials=/path/credentialfile
```
Format:
![[Pasted image 20240919003745.png]]

Searching for string in file name
```shell-session
find /mnt/Finance/ -name *STRING*
```

Searching for string in file 
```shell-session
grep -rn /mnt/Finance/ -ie STRING
```



