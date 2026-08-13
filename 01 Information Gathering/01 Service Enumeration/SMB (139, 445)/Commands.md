# Nmap scan
```
nmap -p 139,445,137 "$ip" -sVC --script "safe and smb* and not brute" -oN scan/smb_scan_"$ip".txt
```
# Smbclient - connect to share
```
smbclient -N -L //"$ip":/share
```
# SMB null session connect
```
rpcclient -U "" -P "" "$ip"
```
```
rpcclient -U '%' "$ip"
```
- Enum users (access required)
`enumdomusers`
`queryuser <rid>`

- Group information
`querygroup <rid>`


---
#### Full enumeration
```
enum4linux -a "$ip"
enum4linux-ng "$ip"
samrdump.py "$ip"
smbmap -H "$ip"
```
#### One-Line - SMB session check (null, guest, random user) 
```
enum4linux -a -u "" -p "" "$ip" && enum4linux -a -u "guest" -p "" "$ip" && enum4linux -a -u "randUser" -p "" "$ip"
```

```
enum4linux-ng "$ip" -R 2000 -G -u "" -p "" && enum4linux-ng "$ip" -R 2000 -G -u "randUser" -p "" && enum4linux-ng "$ip" -R 2000 -G -u "guest" -p ""
```

#### Detect smb server version
1. `MSF module - smb_version`
			OR
2. [smb_version.sh](https://raw.githubusercontent.com/r0hna/scripts/refs/heads/main/smb_version.sh)
3. [smb-scanner](https://github.com/ntfndOfficial/smbscanner)

---
### Random User login check
```
netexec smb "$ip" -u anonymous -p ""
```
### Guest login check
```
netexec smb "$ip" -u guest -p ""
```
```
smbclient -U 'guest%' -L //"$ip"
```
### Null/anonymous User login check
```
netexec smb "$ip" -u "" -p ""
```
```
smbclient -U '%' -L //"$ip"
```
### Enum groups
```
nxc smb "$ip" -u <username> -p <password> --groups
```
```
nxc smb "$ip" --loggedon-users -u <username> -p <password> --groups
```

```
rpcclient -U "" -N "$ip"
>> enumdomgroups
>> enumdomains
>> querydominfo
```
### SMB share enum
###### Null user
```
smbclient -N -L //"$ip"
```
###### List shares recursively
```
smbmap -r -u "" -p "" -H "$ip"
```
###### Connect with a share
```
smbclient //"$ip"/notes
```
###### List shares
```
smbclient -L "$ip" -N
```
###### List share with creds
```
smbclient -U 'admin%' -L //"$ip"/C$
```
###### SMB2 session check
```
smbclient -L \\\\"$ip"\\ -m SMB2
```
###### List shares
```
smbclient -L //"$ip" -N -c 'recurse;ls'
```
###### List recursively
```
smbmap -H "$ip" -R Folder
```

**Using `.ccache` file for auth**
```
nxc smb dc.rustykey.htb --use-kcache --users
```
```
nxc smb dc.rustykey.htb -k --shares
```
---
### Username enum (RID)
```
ldap_query=$(echo $domain | awk -F. '{print "DC="$1",DC="$2}');ldapsearch -x -b "$ldap_query" -s sub "(&(objectclass=user))" -H  ldap://"$ip" | grep -i samaccountname: | cut -f 2 -d " "
```

```
impacket-lookupsid -no-pass anonymous@"$ip" 5000
```
```
impacket-samrdump "$ip"
```

```
nxc smb "$ip" -u '' -p '' --users-export enum_users.txt
```

```
impacket-lookupsid -no-pass "$domain"
```
						OR
```
for i in $(seq 500 1100);do rpcclient -N -U "" "$ip" -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```

```
MSF module - smb_lookupsid
```

```
nxc smb "$ip" -u guest -p "" --rid-brute
```

```
ridenum "$domain" 500 50000
```

```
impacket-lookupsid -no-pass "guest@$domain" 10000 | grep 'SidTypeUser' | grep -v -e "$domain" | awk -F'\\' '{print $2}' | sed 's/ (SidTypeUser)//'
```

```
rpcclient -U "" -N "$ip"
$>> enumdomusers
```

---
### Alternative tools
	○ Enum4linux
		enum4linux "$ip" -A

	○ Samrdump.py
		samrdump.py "$ip"

	○ smbmap
		smbmap -H "$ip"

	○ CrackMapExec
		nxc smb "$ip" --shares -u '' -p ''

### Tools to connect with smb machine
	nxc
	psexec (metasploit)
	winexec
	psexec.py
	smbexec.py
	wmiexec.py
	RDP connection

### Download smb file/dir
	smbclient //"$ip"/users
	>mask ""
	>prompt
	>recurse
	>mget *
			OR
	smb: > mget *

