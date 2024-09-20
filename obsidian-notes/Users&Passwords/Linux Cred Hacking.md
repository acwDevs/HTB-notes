
Editing etc/passwd
	Remove X from etc/passwd to not fetch password from etc/shadow
	
	![[Pasted image 20240915121205.png]]



![[Pasted image 20240915122756.png]]
```shell-session
sudo cp /etc/passwd /tmp/passwd.bak 
sudo cp /etc/shadow /tmp/shadow.bak 
unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes
```

![[Pasted image 20240915122843.png]]
```shell-session
hashcat -m 1800 -a 0 /tmp/unshadowed.hashes rockyou.txt -o /tmp/unshadowed.cracked
```
