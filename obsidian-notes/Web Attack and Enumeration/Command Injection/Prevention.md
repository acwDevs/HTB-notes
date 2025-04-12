
### Input Validation

filter validation
```php
if (filter_var($_GET['ip'], FILTER_VALIDATE_IP)) {
    // call function
} else {
    // deny request
}
```

regex validation
```javascript
if(/^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/.test(ip)){
    // call function
}
else{
    // deny request
}
```



### Input Sanitization
```php
$ip = preg_replace('/[^A-Za-z0-9.]/', '', $_GET['ip']);
```
```javascript
var ip = ip.replace(/[^A-Za-z0-9.]/g, '');
```
[nodeJS module]
```javascript
import DOMPurify from 'dompurify';
var ip = DOMPurify.sanitize(ip);
```


### Server Configuration

- Use the web server's built-in Web Application Firewall (e.g., in Apache `mod_security`), in addition to an external WAF (e.g. `Cloudflare`, `Fortinet`, `Imperva`..)
    
- Abide by the [Principle of Least Privilege (PoLP)](https://en.wikipedia.org/wiki/Principle_of_least_privilege) by running the web server as a low privileged user (e.g. `www-data`)
    
- Prevent certain functions from being executed by the web server (e.g., in PHP `disable_functions=system,...`)
    
- Limit the scope accessible by the web application to its folder (e.g. in PHP `open_basedir = '/var/www/html'`)
    
- Reject double-encoded requests and non-ASCII characters in URLs
    
- Avoid the use of sensitive/outdated libraries and modules (e.g. [PHP CGI](https://www.php.net/manual/en/install.unix.commandline.php))