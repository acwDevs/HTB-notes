
local port forwarding via ssh
```shell-session
ssh -L 1234:localhost:3306 ubuntu@10.129.202.64
```

Multiple port forwarding via ssh
```shell-session
ssh -L 1234:localhost:3306 -L 8080:localhost:80 ubuntu@10.129.202.64
```

`-L` command tells the SSH client to request the SSH server to forward all the data we send via the port `1234` to `localhost:3306` on the Ubuntu server


## SSH Tunneling over SOCKS proxy

Dynamic port forwarding with ssh (edit proxychains config file)
```shell-session
ssh -D 9050 ubuntu@10.129.202.64


nano etc/proxychains.conf
```

The `-D` argument requests the SSH server to enable dynamic port forwarding. Once we have this enabled, we will require a tool that can route any tool's packets over the port `9050`. We can do this using the tool `proxychains`. To inform proxychains that we must use port 9050, we must modify the proxychains configuration file located at `/etc/proxychains.conf`. We can add `socks4 127.0.0.1 9050` to the last line if it is not already there.

Running nmap over proxychains
```shell-session
proxychains nmap -v -sn 172.16.5.1-200
```
