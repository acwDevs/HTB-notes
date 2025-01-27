mysql
```shell-session
mysql -u root -h docker.hackthebox.eu -P 3306 -p 
```

Create DB
```SQL
CREATE DATABASE users;
```

Show DB's
```SQL
SHOW DATABASES;
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
```SQL
DROP TABLE logins;
```

Alter
```SQL
ALTER TABLE logins ADD newColumn INT;
```

Update
```sql
UPDATE table_name SET column1=newvalue1, column2=newvalue2, ... WHERE <condition>;
```

