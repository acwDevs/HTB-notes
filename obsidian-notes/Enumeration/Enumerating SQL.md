
### SQL Common Ports
1433
1434
3306
2433

### Default Databases

`MySQL` default system schemas/databases:

- `mysql` - is the system database that contains tables that store information required by the MySQL server
- `information_schema` - provides access to database metadata
- `performance_schema` - is a feature for monitoring MySQL Server execution at a low level
- `sys` - a set of objects that helps DBAs and developers interpret data collected by the Performance Schema

`MSSQL` default system schemas/databases:

- `master` - keeps the information for an instance of SQL Server.
- `msdb` - used by SQL Server Agent.
- `model` - a template database copied for each new database.
- `resource` - a read-only database that keeps system objects visible in every database on the server in sys schema.
- `tempdb` - keeps temporary objects for SQL queries.


nmap scan
```shell-session
nmap -Pn -sV -sC -p1433 10.10.10.125
```

Connecting to mysql
```shell-session
mysql -u julio -pPassword123 -h 10.129.20.13
```

Connecting to SQL server
```cmd-session
sqlcmd -S SRVMSSQL -U julio -P 'MyPassword!' -y 30 -Y 30
```

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
