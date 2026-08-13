```
cat /etc/ssh/sshd_config  | grep -v "#" | sed -r '/^\s*$/d'
```