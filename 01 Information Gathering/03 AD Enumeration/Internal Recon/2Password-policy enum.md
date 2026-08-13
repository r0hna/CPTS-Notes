# From Linux
#### Netexec 
```
nxc smb 172.16.5.5 -u user -p password --pass-pol
```

#### rpcclient 
```
rpcclient -U "" -N "$ip"
> querydominfo 
> getdompwinfo
```
#### Enum4linux 
```
enum4linux -P "$ip"
```

#### Enum4linux-ng 
```
enum4linux-ng -P "$ip" -oA "$out"
```
```
enum4linux-ng -A "$domain"
```
#### ldapsearch 
```
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```

---
# From Windows 

#### Check NULL session 
```
net use \\DC01\ipc$ "" /u:""
```
#### Authenticate with share
```
net use \\DC01\ipc$ "password" /u:guest
```

#### Enumerate password policy 
If we can authenticate to domain from a windows host, we can use built-in windows tool such as net.exe.
If we can transfer tools to windows host we can use various tools such as powerview, crackmapexec, `sharpmapexec`, `sharpview`, etc. 

- Net.exe 
```
net accounts
```

- Powerview.ps1 
```
Import-module .\powerview.ps1
```
```
Get-DomainPolicy
```