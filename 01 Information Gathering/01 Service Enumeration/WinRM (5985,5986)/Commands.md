# Nmap scan
```
nmap -sV -sC "$ip" -p5985,5986 --disable-arp-ping -n
```

# Win-rm
### Connect with server
```
evil-winrm -i "$domain" -u Cry0l1t3 -p P455w0rD!
```
# WMI
```
impacket-wmiexec Cry0l1t3:"P455w0rD!"@"$ip" "hostname"
```

