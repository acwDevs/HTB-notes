nmap script can be used (-sC does this automatically)

```
ftp-anon
```
Source:https://nmap.org/nsedoc/scripts/ftp-anon.html

Login Bruteforcing Tools
	hydra
		https://github.com/vanhauser-thc/thc-hydra
	medusa
		https://github.com/jmk-foofus/medusa

\
Medusa example
```shell-session
medusa -u fiona -P /usr/share/wordlists/rockyou.txt -h 10.129.203.7 -M ftp
```


Scanning internal ftp servers using ftp bounce attack (nmap -b)
```shell-session
nmap -Pn -v -n -p80 -b anonymous:password@10.10.110.213 172.17.0.2
```


Exploiting COREFTP with improperly handled put request

Changed.