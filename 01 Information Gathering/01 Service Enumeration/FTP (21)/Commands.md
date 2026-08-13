# Enumeration
#### nmap 
```
sudo nmap -p21 -sVC -A --script ftp* "$ip"
```
#### Service interaction
```
nc -nv "$ip" 21
telnet "$ip" 21
openssl s_client -connect "$ip" -starttls ftp
```

---
#### Anonymous access check
```
ftp anonymous@"$ip"
```
#### FTP features enumeration
```
nmap -p 21 --script ftp-features "$ip"
```
#### Download all files
```
wget -m --no-passive ftp://anonymous:anonymous@"$ip"
```
#### Information gather
```
>status
>debug
>trace
```

# Login to ftp
```
ftp ftp://ftpuser:<FTPUSER_PASSWORD>@localhost
```