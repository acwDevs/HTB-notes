

Common info files
```shell-session
>for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*");do echo -e "\nFile extension: " $ext; find / -name *$ext 2>/dev/null | grep -v "lib\|fonts\|share\|core" ;done
```


SSH Keys
```shell-session
>grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"
```
```shell-session
>cat /home/cry0l1t3/.ssh/SSH.private
```

Finding john hashing scripts
```shell-session
>locate *2john*
```

Cracking ssh
```shell-session
>john --wordlist=rockyou.txt ssh.hash
```

Showing cracked passwords
```shell-session
>john ssh.hash --show
```

Cracking Microsoft Office Documents
```shell-session
>office2john.py Protected.docx > protected-docx.

>john --wordlist=rockyou.txt protected-docx.hash

```

Cracking pdf
```shell-session
>pdf2john.py PDF.pdf > pdf.hash

>john --wordlist=rockyou.txt pdf.hash
```
