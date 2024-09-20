https://hashcat.net/wiki/doku.php?id=example_hashes

https://github.com/frizb/Hashcat-Cheatsheet



Creating mutated password list
```shell-session
hashcat --force password.list -r custom.rule --stdout | sort -u > mut_password.list
```
![[Pasted image 20240911010651.png]]
![[Pasted image 20240911010725.png]]
