# Nmap Scan
```
nmap -p 22 "$ip" -sVC --script ssh* -oN ssh_scan.txt
```

#### Grab ssh_rsa key (nmap)
```
nmap "$ip" -p 22 --script ssh-hostkey --script-args ssh_hostkey=full
```

# Footprinting (audit)
```
git clone https://github.com/jtesta/ssh-audit.git && cd ssh-audit
./ssh-audit.py "$ip"
```
#### Find out the key (`id_rsa`) belong to which user
#ssh-keygen #key #id_rsa
```
ssh-keygen -y -f id_rsa
```

# Specify auth method
```
ssh -v cry0l1t3@"$ip" -o PreferredAuthentications=password
```