
nmap
```shell-session
sudo nmap 10.129.14.128 -sV -sC -p139,445
```

List out file shares available via null session
```shell-session
smbclient -N -L //10.129.14.128
```

Get permissions on each share
```shell-session
smbmap -H 10.129.14.128
```

Browsing files in shares recursively
```shell-session
smbmap -H 10.129.14.128 -r notes
```

Password spraying with crackmapexec
```shell-session
crackmapexec smb 10.10.110.17 -u /tmp/userlist.txt -p 'Company01!' --local-auth
```

Enumerating logged in users 
```shell-session
crackmapexec smb 10.10.110.0/24 -u administrator -p 'Password123!' --loggedon-users
```

Automated enumeration tool
	Written in perl
		https://github.com/CiscoCXSecurity/enum4linux
	Written in python
		https://github.com/cddmp/enum4linux-ng