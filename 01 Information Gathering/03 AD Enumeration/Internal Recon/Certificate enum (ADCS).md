# Enumerate active directory certificate (ADCS) 
Source: [Windows PrivEsc with AD CS | Exploit Notes](https://exploit-notes.hdks.org/exploit/windows/privilege-escalation/windows-privesc-with-adcs/) 

#### Find the vulnerable template 
```
certipy find -u ca_svc@sequel.htb -hashes :3b181b914e7a9d5508xxxxxxxxxxx -stdout -vulnerable
```
        OR 
```
certipy find -u raven -p 'R4v3nBe5tD3veloP3r!123' -dc-ip 10.10.11.236 -stdout -vulnerable
```

>Also run `certify.exe` from windows machine as well.
