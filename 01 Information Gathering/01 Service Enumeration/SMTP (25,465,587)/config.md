# Default config
```
cat /etc/postfix/main.cf | grep -v "#" | sed -r "/^\s*$/d"
```