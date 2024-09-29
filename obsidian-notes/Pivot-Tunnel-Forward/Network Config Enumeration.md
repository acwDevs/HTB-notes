

Searching NIC's
	ifconfig
	ipconfig
	ip -a

Inspect routing tables
	netstat -r 
	ip route

Checking port forward with netstat
```shell-session
netstat -antp | grep 1234
```
Checking port forward with nmap
```shell-session
nmap -v -sV -p1234 localhost
```
