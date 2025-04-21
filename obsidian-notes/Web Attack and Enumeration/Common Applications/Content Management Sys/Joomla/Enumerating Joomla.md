
querying joomla api for statistics
```shell-session
curl -s https://developer.joomla.org/stats/cms_version | python3 -m json.tool
```

searching for joomla in website output
```shell-session
curl -s http://dev.inlanefreight.local/ | grep Joomla
```

getting joomla version via readme
```shell-session
curl -s http://dev.inlanefreight.local/README.txt | head -n 5
```


##### Common directories
-  /media/system/js/
- /administrator/manifests/files/joomla.xml
-  /plugins/system/cache/cache.xml


#### Automated Scanning

 [droopescan](https://github.com/droope/droopescan)

default usage
```shell-session
droopescan scan joomla --url http://dev.inlanefreight.local/
```

[JoomlaScan](https://github.com/drego85/JoomlaScan)

default usage
```shell-session
python2.7 joomlascan.py -u http://dev.inlanefreight.local
```

[Joomla login bruteforce](https://github.com/ajnik/joomla-bruteforce)

default usage
```shell-session
sudo python3 joomla-brute.py -u http://dev.inlanefreight.local -w /usr/share/metasploit-framework/data/wordlists/http_default_pass.txt -usr admin
```
