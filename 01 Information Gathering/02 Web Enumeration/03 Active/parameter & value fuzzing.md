# Fuzz a URL parameter to access a protected page

#### Get Request (key fuzzing)
```
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt -u http://"$domain"/admin/admin.php?FUZZ=key -mc all
```


---
# Post-Data fuzzing
#### Key fuzzing
```
ffuf -u http://"$domain"/admin/admin.php -mc all -w /usr/share/seclists/Discovery/web-content/burp-parameter-names.txt -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded'
```
#### Value fuzzing
```
ffuf -u http://"$domain"/admin/admin.php -mc all -w num.list -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'
```
#### Value fuzzing (numbers)
```
ffuf -X POST -u http://"$domain"/admin/admin.php -mc all -w num.list -d 'username=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'
```
