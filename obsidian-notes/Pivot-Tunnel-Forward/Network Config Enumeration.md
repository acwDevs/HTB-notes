

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

Ping sweep for host on subnet
```shell-session
run post/multi/gather/ping_sweep RHOSTS=172.16.5.0/23
```
```shell-session
for i in {1..254} ;do (ping -c 1 172.16.5.$i | grep "bytes from" &) ;done
```
```cmd-session
for /L %i in (1 1 254) do ping 172.16.5.%i -n 1 -w 100 | find "Reply"
```