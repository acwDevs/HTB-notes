
[Jenkins](https://www.jenkins.io/) is an open-source automation server written in Java that helps developers build and test their software projects continuously. It is a server-based system that runs in servlet containers such as Tomcat.

Jenkins runs on Tomcat port 8080 by default. It also utilizes port 5000 to attach slave servers.


We can fingerprint Jenkins quickly by the telltale login page.
```url
http://jenkins.inlanefreight.local:8000/login?from=%2F
```
