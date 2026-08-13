# Finding kerberos tickets in linux (keytab file) 
```
Linikatz.sh
```
```
find / -name *keytab* -ls 2>/dev/null
```
```
find / -name krb5cc_* -ls 2>/dev/null
```
```
find / -name *.kt -ls 2>/dev/null     #ccache file
```
```
crontab -l 
```