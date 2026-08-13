# Nmap scan
```
sudo nmap "$ip" -sV -sC -p3306 --script mysql*
```
#### MySQL capabilities check
```
nmap -p 3306 "$ip" -sV --script mysql-info --script-args 'mysqluser=root, mysqlpass=""'
```

## Connect to SQL server
```
mysql -U julio -pPasssword123 -h "$ip"
```


## Connect to mysql server
```
mysql -h "$ip" -u root -p<pass>
```
```
mysql -U root -p<password> -h "$ip"
```
								OR
```
mysql -D 'wordpress' -u 'wp_user' -h "$ip" --skip-ssl -p              # skip ssl
```
								OR
```
C:\xampp\mysql\bin\mysql.exe -u MrGibbonsDB -p"MisterGibbs!Parrot!?1"
```

>sometime double-quote solve problem in windows


# MySQL Commands
#### MySQL readable file check
```
msfconsole > search 'auxiliary/scanner/mysql/mysql_file_enum'
```

#### Load a system file in MySQL
```
select load_file('/etc/shadow');
```

#### MySQL file privileges check
```
nmap -p 3306 --script mysql-audit --script-args "mysql-audit.username='root',mysql-audit.password='',mysql-audit.filename='/usr/share/nmap/nselib/data/mysql-cis.audit'" "$ip"
```

#### Run mysql commands with nmap
```
nmap -p 3306 --script mysql-query --script-args 'username=root, password="", query="select count(\*) from books.authors;"' "$ip"
```

#### Mysql config
```
cat /etc/mysql/mysql.conf.d/mysqld.cnf
```

