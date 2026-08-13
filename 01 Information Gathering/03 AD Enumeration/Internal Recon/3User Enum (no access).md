#### Enum4linux 
```
enum4linux -U "$ip"  | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
```
        OR 
```
enum4linux-ng -P "$ip" -oA "$out"
```
#### RPC-Client 
```
rpcclient -U "" -N "$ip" -c "enumdomusers; querydominfo; exit"
```
#### RID enum 
```
for i in $(seq 500 50000);do rpcclient -N -U "" "$ip" -c "queryuser 0x$(printf '%x\n' $i)"|grep "User Name\|user_rid\|group_rid" && echo "";done
```
        OR 
```
ridenum "$ip" 500 50000
```
#### Kerbrute
```
kerbrute userenum -d "$domain" --dc "$ip" /opt/jsmith.txt -o valid_ad_users.txt
```

#### Netexec 
```
nxc smb "$ip" --users
```
```
nxc smb "$ip" -u user -p password --users
```
#### Impacket 
```
impacket-lookupsid -no-pass domain.local
```
#### ldapsearch
```
ldapsearch -h "$ip" -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "
```
```
ldapsearch -x -b "DC=active,DC=htb" -s sub "(&(objectclass=user))" -H ldap://active.htb | grep sAMAccountName: | cut -f2 -d" "
```
#### ldapsearch (list all AD objects)
#alladobject #listalladject #ldapsearch
```
ldapsearch -x -H ldap://192.168.210.4 -D "mellon@internal.xyz.local" -w password -b "dc=internal,dc=xyz,dc=local"
```

#### Windapsearch 
```
windapsearch --dc-ip "$ip" -u "" -U
```
```
windapsearch -m users -u '' -p '' -d "$ip"
```
#### kerbrute
```
kerbrute userenum -d inlanefreight.local --dc "$ip" /opt/jsmith.txt
```

---

# Detailed user enum
- By leveraging an SMB NULL session to retrieve a complete list of domain users from the domain controller
- Utilizing an LDAP anonymous bind to query LDAP anonymously and pull down the domain user list
- Using a tool such as `Kerbrute` to validate users utilizing a word list from a source such as the [statistically-likely-usernames](https://github.com/insidetrust/statistically-likely-usernames) GitHub repo, or gathered by using a tool such as [linkedin2username](https://github.com/initstring/linkedin2username) to create a list of potentially valid users
- Using a set of credentials from a Linux or Windows attack system either provided by our client or obtained through another means such as LLMNR/NBT-NS response poisoning using `Responder` or even a successful password spray using a smaller wordlist.

---
# Tip
We've checked over 48,000 usernames in just over 12 seconds and discovered 50+ valid ones. Using `Kerbrute` for username enumeration will generate event ID [4768: A Kerberos authentication ticket (TGT) was requested](https://docs.microsoft.com/en-us/windows/security/threat-protection/auditing/event-4768). This will only be triggered if [Kerberos event logging](https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/enable-kerberos-event-logging) is enabled via Group Policy. Defenders can tune their SIEM tools to look for an influx of this event ID, which may indicate an attack. If we are successful with this method during a penetration test, this can be an excellent recommendation to add to our report.

If we are unable to create a valid username list using any of the methods highlighted above, we could turn back to external information gathering and search for company email addresses or use a tool such as [linkedin2username](https://github.com/initstring/linkedin2username) to mash up possible usernames from a company's LinkedIn page.