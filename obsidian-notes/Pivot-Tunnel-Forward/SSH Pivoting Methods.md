
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