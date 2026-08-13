#timerestriction #logonhours #loginrestriction
```
Set-ADUser -Identity "javier.mmarshall" -Clear logonHours
```
									OR
```
#File: ldif
dn: CN=John Doe,CN=Users,DC=yourdomain,DC=com
changetype: modify
delete: logonHours


ldapmodify -H ldap://dc1.yourdomain.com -D "cn=Administrator,cn=Users,dc=yourdomain,dc=com" -W -f clear_logon_hours.ldif
```
									OR
```
certipy-ad account update -u javier.mmarshall@mirage.local -p 'NewPass123!' -user javier.mmarshall -logon-hrs-clear -dc-ip 10.10.10.10
```