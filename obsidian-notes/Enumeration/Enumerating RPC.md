
Creating RPC null session
```shell-session
>rpcclient -U'%' 10.10.110.17
```

After session creation we can enumerate users
```shell-session
 rpcclient> enumdomusers
```

Automated enumeration tool
	Written in perl
		https://github.com/CiscoCXSecurity/enum4linux
	Written in python
		https://github.com/cddmp/enum4linux-ng


