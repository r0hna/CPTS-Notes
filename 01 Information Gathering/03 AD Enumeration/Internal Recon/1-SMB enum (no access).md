# SMB Null sessions check
#### [[CPTS Notes/01 Information Gathering/01 Service Enumeration/SMB (139, 445)/Commands|Commands]]

#### check password in gpp
```
nxc smb "$ip" -u user -p pass -M gpp_password
```
#### Check SMB share
>It is important to check SMB share manually.
```
nxc smb "$ip" -u user -p pass -M spider_plus
```

