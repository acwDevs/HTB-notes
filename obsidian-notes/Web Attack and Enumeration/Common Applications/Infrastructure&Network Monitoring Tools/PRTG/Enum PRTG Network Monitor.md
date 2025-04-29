
We can quickly discover PRTG from an Nmap scan. It can typically be found on common web ports such as 80, 443, or 8080. It is possible to change the web interface port in the Setup section when logged in as an admin.

nmap scan for PRTG
```shell-session
sudo nmap -sV -p- --open -T4 10.129.201.50
```

default credentials

| user      | pass      |
| --------- | --------- |
| prtgadmin | prtgadmin |

[nessus plugin for vuln scan](https://www.tenable.com/plugins/nessus/51874)


curl to check version information
```shell-session
curl -s http://10.129.201.50:8080/index.htm -A "Mozilla/5.0 (compatible;  MSIE 7.01; Windows NT 5.0)" | grep version
```
