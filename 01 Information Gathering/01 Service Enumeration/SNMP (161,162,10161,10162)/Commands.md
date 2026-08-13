# Nmap scan
```
sudo nmap -sU -p 161 --script snmp-brute "$ip"
```
#### Enum SNMP OIDs
```
nmap -sU -p 161 --script snmp-interfaces "$ip"
```

# Enumeration
>Default strings `public` and `private`. Try them both with tools
#### Brute force community string
```
onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp.txt  "$ip"
```

#### Enum SNMP information
```
snmpwalk -v2c -c <public> "$ip"
```

```
braa <string>@"$ip":.1.3.6.*     #<private>
```

```
snmpwalk -v 2c -c public "$ip" 1.3.6.1.2.1.1.5.0
```

```
snmp-check -c public "$ip"
```

```
MSF module - use auxiliary/scanner/snmp/snmp_enum
```

---

#### If "writable" string is present
```
snmpset -v 2c -c private "$ip" 1.3.6.1.2.1.1.5.0 s "NewHostName"
```
#### Collect system information
```
snmpwalk -v 2c -c public "$ip" 1.3.6.1.2.1.1
```

#### OIDs enum
```
MSF module - use use auxiliary/scanner/snmp/snmp_set
```
