>Hack Tricks: [1433 - Pen-testing MSSQL - Microsoft SQL Server - HackTricks](https://book.hacktricks.wiki/en/network-services-pentesting/pentesting-mssql-microsoft-sql-server/index.html)

# Nmap scan
```
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER,ms-sql-xp-cmdshell.cmd='whoami' -sV -p 1433 "$ip"
```
# Connect to mssql
```
impacket-mssqlclient Administrator@"$ip" -windows-auth
```
```
sqlcmd -S SRVMSSQL -U julio -P 'password!' -y 30 -Y 20 (windows)
```
#### Connect to Ms-SQL server
```
sqsh -S "$ip" -U julio -P 'password!' -h
```
```
sqsh -S "$ip" -U .\\julio -P 'mypassword!' -h (with domain name)
```
#### Impacket tool
```
Impacket-mssqlclient -p 1433 julio@"$ip"
```
# MSF Enum
```
mssql_ping
mssql_ntlm_stealer
mssql_payload
mssql_enum_domain_accounts
mssql_enum_sql_logins
mssql_findandsampledata
mssql_hashdump
mssql_schemadump
```

#### Database commands
```
select name from sys.databases;  # show all database
```
