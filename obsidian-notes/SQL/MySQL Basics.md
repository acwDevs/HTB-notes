mysql
```shell-session
mysql -u root -h docker.hackthebox.eu -P 3306 -p 
```

Create DB
```shell-session
mysql> CREATE DATABASE users;
```

Show DB's
```shell-session
mysql> SHOW DATABASES;
```

Insert
```sql
INSERT INTO table_name VALUES (column1_value, column2_value, column3_value, ...);
```

Select
```sql
SELECT * FROM table_name;
```

Drop
```shell-session
DROP TABLE logins;
```

Alter
```shell-session
ALTER TABLE logins ADD newColumn INT;
```

Update
```sql
UPDATE table_name SET column1=newvalue1, column2=newvalue2, ... WHERE <condition>;
```

