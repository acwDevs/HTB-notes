
nmap scan
```shell-session
nmap -p53 -Pn -sV -sC 10.10.110.213
```


Zone transfer enum with dig
```shell-session
dig AXFR @ns.inlanefreight.htb inlanefreight.htb
```


https://github.com/mschwager/fierce
```shell-session
fierce --domain zonetransfer.me
```


Subdomain enumeration
https://github.com/projectdiscovery/subfinder
```shell-session
./subfinder -d inlanefreight.com -v
```

https://github.com/aboul3la/Sublist3r

Good for finding subdomain offline (We like this one a lot)
https://github.com/TheRook/subbrute
```shell-session
Auzzie@htb[/htb]$ git clone https://github.com/TheRook/subbrute.git >> /dev/null 2>&1
Auzzie@htb[/htb]$ cd subbrute
Auzzie@htb[/htb]$ echo "ns1.inlanefreight.com" > ./resolvers.txt
Auzzie@htb[/htb]$ ./subbrute inlanefreight.com -s ./names.txt -r ./resolvers.txt
```

cname record enumeration
```shell-session
host support.inlanefreight.com

or 

nslookup support.inlanefreight.com
```


Check for subdomain takeover vulnerability
https://github.com/EdOverflow/can-i-take-over-xyz

Local DNS cache poisoning with ettercap or bettercap
https://www.ettercap-project.org/
https://www.bettercap.org/

Add domain to file

```shell-session
Auzzie@htb[/htb]# cat /etc/ettercap/etter.dns

inlanefreight.com      A   192.168.225.110
*.inlanefreight.com    A   192.168.225.110
```