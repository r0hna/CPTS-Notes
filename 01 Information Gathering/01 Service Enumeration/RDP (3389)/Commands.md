# Nmap Scan
```
nmap -sVC --script rdp* "$ip" -p3389 --disable-arp-ping -n
```

# RDP security check 
>module installation
```
sudo cpan
```
#### Download tool
```
git clone https://github.com/CiscoCXSecurity/rdp-sec-check.git && cd rdp-sec-check
```
```
./rdp-sec-check.pl "$ip"
```

# RDP connect
1. `xfreerdp3`
```
xfreerdp3 /u:cry0l1t3 /p:"P455w0rd!" /v:"$ip" 
```
2. `remmina`
3. `rdedktop`
