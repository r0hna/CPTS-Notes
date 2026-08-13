# Netexec
```
sudo nxc smb "$ip" -u htb-student -p Academy_student_AD! --users
```
# Windapsearch 
#### Domain admin enumeration 
```
Impacket-windapsearch --dc-ip 172.16.5.5 -u forend@inalnefreight.lcoal -p klmcargo2 --da
```
#### Privileged user enumeration 
```
Impacket-windapsearch --dc-ip 172.16.5.5 -u forend@inalnefreight.lcoal -p klmcargo2 -PU
```

---
# Enumeration (after acquired foothold in the domain)
#### Netexec 
- Domain user enumeration 
```
sudo nxc smb 172.16.5.5 -u forend -p klmcargo3 --users
```

- Domain group enumeration 
```
sudo nxc ldap 172.16.5.5 -u forend -p klmcargo3 --groups
```

- Logged on users 
```
sudo nxc smb 172.16.5.5 -u forend -p klmcargo3 --loggedon-users
```

- Enum share (DC) 
```
sudo nxc smb 172.16.5.5 -u forend -p klmcargo3 --shares
```

- Search information inside share 
```
sudo nxc smb 172.16.5.5 -u forend -p klmcargo3 -M spider_plus --share 'Department shares'
```
---
#### Smbmap 
#smbmap
- Access check 
```
smbmap -u forend -p klmcargo2 -d INLANEFREIGHT.LOCAL -H "$ip"
```

- List all directories (recursive) 
```
smbmap -u forend -p klmcargo2 -d INLANEFREIGHT.LOCAL -H <ip> -R 'Department Shares' --dir-only
```
---
#### rpcclient 
- SMB Null session check 
```
rpcclient -U "" -N 172.16.5.5 -c "queryuser 0x457; exit"
```
```
rpcclient -U "" -N 172.16.5.5 -c "enumdomusers; exit"
```
