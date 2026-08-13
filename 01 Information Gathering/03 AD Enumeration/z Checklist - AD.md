# Active Directory Enumeration Checklist (CPTS with DPAPI)

## Domain Information
- [ ] Get current domain and SID:  
  `Get-ADDomain`  
  `Get-DomainSID`
- [ ] List domain controllers and trusted domains:  
  `Get-ADDomainController`  
  `Get-ADTrust -Filter *`

## Domain Users, Groups, and Computers
- [ ] Enumerate all users:  
  `Get-ADUser -Filter * -Properties *`
- [ ] Enumerate domain admins and groups:  
  `Get-ADGroupMember -Identity "Domain Admins"`  
  `Get-ADGroup -Filter *`
- [ ] List domain computers and OUs:  
  `Get-ADComputer -Filter * -Properties *`  
  `Get-ADOrganizationalUnit -Filter *`

## Shares & Permissions
- [ ] List domain shares and access:  
  `Find-DomainShare`  
  `Find-DomainShare -CheckShareAccess`
- [ ] Enumerate interesting files across shares:  
  `Find-InterestingDomainShareFile -Include *passwords*`

## GPOs and ACLs
- [ ] Enumerate Group Policy Objects:  
  `Get-ADGroupPolicy`  
  `Get-DomainGPO -ComputerIdentity <Computer>`
- [ ] Check ACLs for permissions and delegation abuse:  
  `Get-DomainObjectAcl -Identity <ObjectName>`  
  `Find-InterestingDomainAcl`

## SPN & Kerberoasting
- [ ] Find SPNs and potential Kerberoast accounts:  
  `Get-NetUser -SPN`
- [ ] Use Rubeus or PowerView for Kerberoasting attacks

## Session & Logged On Users Information
- [ ] List active sessions and logged on users:  
  `Get-NetSession`  
  `Get-NetLoggedon`

## DPAPI Enumeration and Extraction
- [ ] Locate DPAPI storage paths:  
  `C:\Users\$USER\AppData\Roaming\Microsoft\Protect\$SUID\$GUID`  
  `C:\Users\$USER\AppData\Local\Microsoft\Credentials`  
  `C:\Users\$USER\AppData\Roaming\Microsoft\Credentials`
- [ ] Extract and decrypt DPAPI master keys and credentials using tools:  
  - `dpapi.py masterkey -file <masterkey_file> -sid <user_SID> -password <masterkey_password>`  
  - `dpapi.py backupkeys -t <domain/user:password@target>`  
  - `dpapi.py credential -file <protected_file> -key <masterkey>`  
  - DonPAPI for remote DPAPI secret extraction:  
    `DonPAPI.py 'domain/username:password@target'`

## Tools for AD & DPAPI Enumeration
- PowerView
- BloodHound
- Rubeus
- Mimikatz
- Impacket (dpapi.py, secretsdump.py)
- CrackMapExec
- DonPAPI

---

**Recommendations:**  
- Perform iterative enumeration starting broad and narrowing down to sensitive targets.  
- Collect and review DPAPI protected secrets carefully; they often hold valuable credentials like Wi-Fi passwords, RDP secrets, Outlook credentials, or cached domain credentials.  
- Document every stage and findings meticulously for exam reporting.

