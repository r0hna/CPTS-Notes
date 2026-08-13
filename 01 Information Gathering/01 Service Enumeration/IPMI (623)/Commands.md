# Nmap scan
```
sudo nmap -sU --script ipmi-version -p 623 "$ip"
```

# Version scan (msf)
```
search  ipmi_version
```

# IPMI 2.0 RAKP hash-retrieval
```
search ipmi_dumphashes
```
#### Crack IPMI hashes
```
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u
```