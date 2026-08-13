# Default
```
cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'
```