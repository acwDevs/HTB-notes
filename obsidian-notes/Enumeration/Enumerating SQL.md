
Cheat Sheet
https://learnsql.com/blog/sql-server-cheat-sheet/
https://gist.github.com/bradtraversy/c831baaad44343cc945e76c2e30927b3

### SQL Common Ports
1433
1434
3306
2433

nmap scan
```shell-session
nmap -Pn -sV -sC -p1433 10.10.10.125
```


### Default Databases

`MySQL` default system schemas/databases:

- `mysql` - is the system database that contains tables that store information required by the MySQL server
- `information_schema` - provides access to database metadata
- `performance_schema` - is a feature for monitoring MySQL Server execution at a low level
- `sys` - a set of objects that helps DBAs and developers interpret data collected by the Performance Schema


Connecting to mysql
```shell-session
mysql -u julio -pPassword123 -h 10.129.20.13
```

Connecting to SQL server
```cmd-session
sqlcmd -S SRVMSSQL -U julio -P 'MyPassword!' -y 30 -Y 30
```


`MSSQL` default system schemas/databases:

- `master` - keeps the information for an instance of SQL Server.
- `msdb` - used by SQL Server Agent.
- `model` - a template database copied for each new database.
- `resource` - a read-only database that keeps system objects visible in every database on the server in sys schema.
- `tempdb` - keeps temporary objects for SQL queries.


MSSQL from Linux
```shell-session
sqsh -S 10.129.203.7 -U julio -P 'MyPassword!' -h
```
```shell-session
mssqlclient.py -p 1433 julio@10.129.203.7 
```

MSSQL using windows authentication mode (".\\\\julio")
```shell-session
sqsh -S 10.129.203.7 -U .\\julio -P 'MyPassword!' -h
```

Show Databases
```cmd-session
1> SELECT name FROM master.dbo.sysdatabases
2> GO
```

Reading Local Files
```cmd-session
1> SELECT * FROM OPENROWSET(BULK N'C:/Windows/System32/drivers/etc/hosts', SINGLE_CLOB) AS Contents
2> GO
```



MSSQL Finding Linked Servers (`1` means is a remote server, and `0` is a linked server)
```cmd-session
1> SELECT srvname, isremote FROM sysservers
2> GO
```

Identifying Users Connecting to Linked Servers
```cmd-session
1> EXECUTE('select @@servername, @@version, system_user, is_srvrolemember(''sysadmin'')') AT [10.0.0.12\SQLEXPRESS]
2> GO
```

