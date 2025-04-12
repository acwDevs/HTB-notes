
 [Bashfuscator](https://github.com/Bashfuscator/Bashfuscator) [linux]
```shell-session
Auzzie@htb[/htb]$ git clone https://github.com/Bashfuscator/Bashfuscator
Auzzie@htb[/htb]$ cd Bashfuscator
Auzzie@htb[/htb]$ pip3 install setuptools==65
Auzzie@htb[/htb]$ python3 setup.py install --user
```


Eg
```shell-session
./bashfuscator -c 'cat /etc/passwd' -s 1 -t 1 --no-mangling --layers 1
```
output
```shell-session
eval "$(W0=(w \  t e c p s a \/ d);for Ll in 4 7 2 1 8 3 2 4 8 5 7 6 6 0 9;{ printf %s "${W0[$Ll]}";};)"
```
verify output
```shell-session
bash -c 'eval "$(W0=(w \  t e c p s a \/ d);for Ll in 4 7 2 1 8 3 2 4 8 5 7 6 6 0 9;{ printf %s "${W0[$Ll]}";};)"'
```



[DOSfuscation](https://github.com/danielbohannon/Invoke-DOSfuscation)  [powershell]
```powershell-session
PS C:\htb> git clone https://github.com/danielbohannon/Invoke-DOSfuscation.git
PS C:\htb> cd Invoke-DOSfuscation
PS C:\htb> Import-Module .\Invoke-DOSfuscation.psd1
PS C:\htb> Invoke-DOSfuscation
```
