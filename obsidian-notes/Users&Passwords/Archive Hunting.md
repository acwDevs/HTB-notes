
Get all file extensions
```shell-session
curl -s https://fileinfo.com/filetypes/compressed | html2text | awk '{print tolower($1)}' | grep "\." | tee -a compressed_ext.txt
```

Cracking with john
```shell-session
zip2john ZIP.zip > zip.hash
```


Display extracted creds with for loop
```shell-session
for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null| tar xz;done
```

Cracking bitlocker drives
```shell-session
>bitlocker2john -i Backup.vhd > backup.hashes

>grep "bitlocker\$0" backup.hashes > backup.hash

>cat backup.hash
```

using hashcat for to crack bitlocker hash
```shell-session
hashcat -m 22100 backup.hash /opt/useful/seclists/Passwords/Leaked-Databases/rockyou.txt -o backup.cracked
```
