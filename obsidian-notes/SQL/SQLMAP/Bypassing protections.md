
CSRF Token Bypass
```shell-session
--csrf-token="CSRF_TOKEN_NAME"
```

Unique value bypass
```shell-session
--randomize=UNIQUE_VALUE_PARAM_NAME
```

Calculated Parameter Bypass(Most likely different on live sites)(Run python script on parameter value)
```shell-session
--eval="import hashlib; h=hashlib.md5(id).hexdigest()"
```

Sending request through proxy to prevent blacklist
```
--proxy="socks4://177.39.187.70:33283"
```

Sending data through tor proxy
```
```