
```shell-session
Auzzie@htb[/htb]$ IP=10.129.42.195
Auzzie@htb[/htb]$ printf "%s\t%s\n\n" "$IP" "app.inlanefreight.local dev.inlanefreight.local blog.inlanefreight.local" | sudo tee -a /etc/hosts
```


