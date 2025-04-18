
##### Screenshot Tools for Mass Web Page Enumeration
[EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness) and [Aquatone](https://github.com/michenriksen/aquatone)

eyewitness usage
```shell-session
eyewitness --web -x web_discovery.xml -d inlanefreight_eyewitness
```

aquatone usage
```shell-session
cat web_discovery.xml | ./aquatone -nmap
```

#### NMAP Scanning Scope on common web app ports
```shell-session
sudo  nmap -p 80,443,8000,8080,8180,8888,10000 --open -oA web_discovery -iL scope_list
```


