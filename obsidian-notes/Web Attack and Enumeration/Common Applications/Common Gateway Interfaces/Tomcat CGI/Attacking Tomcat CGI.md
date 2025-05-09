
The CGI Servlet is a vital component of Apache Tomcat that enables web servers to communicate with external applications beyond the Tomcat JVM. These external applications are typically CGI scripts written in languages like Perl, Python, or Bash. The CGI Servlet receives requests from web browsers and forwards them to CGI scripts for processing.

In essence, a CGI Servlet is a program that runs on a web server, such as Apache2, to support the execution of external applications that conform to the CGI specification. It is a middleware between web servers and external information resources like databases.

#### Finding CGI Scripts

One way to uncover web server content is by utilising the `ffuf` web enumeration tool along with the `dirb common.txt` wordlist. Knowing that the default directory for CGI scripts is `/cgi`, either through prior knowledge or by researching the vulnerability, we can use the URL `http://10.129.204.227:8080/cgi/FUZZ.cmd` or `http://10.129.204.227:8080/cgi/FUZZ.bat` to perform fuzzing.

ffuf commands
```shell-session
ffuf -w /usr/share/dirb/wordlists/common.txt -u http://10.129.204.227:8080/cgi/FUZZ.cmd
```
```shell-session
ffuf -w /usr/share/dirb/wordlists/common.txt -u http://10.129.204.227:8080/cgi/FUZZ.bat
```


#### Exploiting CGI Scripts

For instance, an attacker can append `dir` to a valid command using `&` as a separator to execute `dir` on a Windows system. If the attacker controls the input to a CGI script that uses this command, they can inject their own commands after `&` to execute any command on the server. An example of this is `http://example.com/cgi-bin/hello.bat?&dir`, which passes `&dir` as an argument to `hello.bat` and executes `dir` on the server.

e.g
```http
http://10.129.204.227:8080/cgi/welcome.bat?&dir
```
