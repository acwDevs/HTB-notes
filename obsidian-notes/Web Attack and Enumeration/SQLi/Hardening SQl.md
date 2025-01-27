
Functions
 [mysqli_real_escape_string()](https://www.php.net/manual/en/mysqli.real-escape-string.php)
 [pg_escape_string()](https://www.php.net/manual/en/function.pg-escape-string.php)


Using regular expressions to limit accepted characters
[preg_match()](https://www.php.net/manual/en/function.preg-match.php)
```php
$pattern = "/^[A-Za-z\s]+$/";
$code = $_GET["port_code"];

if(!preg_match($pattern, $code)) {
  die("</table></div><p style='font-size: 15px;'>Invalid input! Please try again.</p>");
}
```

Restrict privileges to only allow select permissions

  