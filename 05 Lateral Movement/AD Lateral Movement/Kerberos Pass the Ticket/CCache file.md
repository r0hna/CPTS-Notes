# Looking for `ccache` files 
```
ls -la /tmp 
```
# METHOD:3 - Impersonating the `ccache` file into current session
#krb5 #klist
```
klist
```
```
cp /tmp/krb5cc_647401106_I8I133 .
```
```
export KRB5CCNAME=/var/lib/sss/db/ccache_INLANEFREIGHT.HTB
```
```
klist
```



