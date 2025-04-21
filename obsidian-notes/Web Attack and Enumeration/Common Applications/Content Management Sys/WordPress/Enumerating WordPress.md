

Searching version info via /robots.txt
```
curl -X GET https://IP:PORT/robots.txt
```

Common Wordpress directories
- /wp-admin
- /wp-content
- /wp-login.php
- wp-content/plugins
- wp-content/themes



#### Standard Wordpress User List

1. Administrator: This user has access to administrative features within the website. This includes adding and deleting users and posts, as well as editing source code.
2. Editor: An editor can publish and manage posts, including the posts of other users.
3. Author: They can publish and manage their own posts.
4. Contributor: These users can write and manage their own posts but cannot publish them.
5. Subscriber: These are standard users who can browse posts and edit their profiles.


### Common Data Commands
```shell-session
curl -s http://blog.inlanefreight.local/ | grep WordPress
```
```shell-session
curl -s http://blog.inlanefreight.local/ | grep themes
```
```shell-session
curl -s http://blog.inlanefreight.local/ | grep plugins
```

### Automated Tools

[WPScan](https://github.com/wpscanteam/wpscan)

Automated content scan with wpscan using api token from [WPVulnDB](https://wpvulndb.com/)
```shell-session
sudo wpscan --url http://blog.inlanefreight.local --enumerate --api-token dEOFB<SNIP>
```

