[PowerView.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1)
[AD Enumeration](https://viperone.gitbook.io/pentest-everything/everything/everything-active-directory/ad-enumeration)
#### Bypass execution policy
```
powershell -ep bypass
```
#### Get all users 
```
Get-NetUser
```
```
net users /domain
```
#### Get all users with filter 
```
Get-NetUser | select cn, memberof
```
#### Get information of a particular user 
```
Get-NetUser -UserName admin
```
#### Get all groups 
```
Get-NetGroup
```
#### User description check
#userdescription #checkuserdescription #bloodyad
```
Get-DomainUser * | Select-Object samaccountname,description |Where-Object {$_.Description -ne $null}
```
```
nxc ldap 10.10.11.32 -u '' -p '' --users | grep 'TypeUser'
```
#### User info field check
#userdescriptioncheck #checkuserdescription #bloodyaduserdescriptioncheck #bloodyad
```
bloodyAD -u ldap -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -d support.htb --host dc.support.htb --dns 10.10.11.174 get search --attr info
```
#### Limit groups to a particular domain 
```
Get-NetGroup -Domain inlanefreight.local
```
#### Get all admin names 
```
Get-NetGroup -AdminCount
```
#### Get all groups a user is member of 
```
Get-NetGroup -UserName admin
```
#### Get specific group's users 
```
Get-NetGroupMember -GroupName "Administrators"
```
#### Get all other computers in the domain 
```
Get-NetComputer
```
#### Check all other computers are online
#livehosts #ping #scanhosts
```
Get-NetComputer -Ping
```
#### Get other computer OS information 
```
Get-NetComputer -fulldata
```
#### Filter out computer OS information 
```
Get-NetComputer -fulldata | select cn, operatingsystem
```
#### Domain enumeration (current domain information) 
```
Get-NetDomain
```
#### Get SID of the current domain 
```
Get-DomainSID
```
#### Get current domain policy 
```
Get-DomainPolicy
```
#### Get domain controller information 
```
Get-NetDomainController
```
#### Which computer we have admin access (IF you are DC) 
```
Find-LocalAdminAccess
```
#### Get all local admins 
```
Invoke-EnumerateLocalAdmin
```
#### Get domain policies 
```
Get-NetGPO
```
#### Get all active sessions/logon users 
```
Get-NetLoggedon -ComputerName domain-controller.inlanefreight.local
```
#### Get last `loggedon` users 
```
Get-LastLoggedon -ComputerName domain-controller.inlanefreight.local
```
#### Get RDP sessions 
```
Get-NetRDPSession -ComputerName domain-controller.inlanefreight.local
```
#### Check recycle bin 
```
[System.IO.Directory]::GetDirectories("C:\`$Recycle.Bin")
```
#### Cheat sheet 
```
https://gist.github.com/HarmJ0y/184f9822b195c52dd50c379ed3117993
```

---
# AD Power-view

#### Get user info 
```
Get-DomainUser -Identity mmorgan -Domain inlanefreight.local | Select-Object -Property name,samaccountname,description,memberof,whencreated,pwdlastset,lastlogontimestamp,accountexpires,admincount,userprincipalname,serviceprincipalname,useraccountcontrol
```
#### Get group membership recursive info 
```
Get-DomainGroupMember -Identity "Domain Admins" -Recurse
```
#### Get domain trust info 
```
Get-DomainTrustMapping
```
#### Testing for local admin/remote admin access 
```
Test-AdminAccess -ComputerName <hostname>
```
#### Find users with SPN set (it may be subjected to a `kerberoasting` attack) 
```
Get-DomainUser -SPN -Properties samaccountname, ServicePrincipleName
```

>`SharpView` is a .NET port of powerview

---
# Useful Power-view commands
| **Command**                         | **Description**                                                                            |
| ----------------------------------- | ------------------------------------------------------------------------------------------ |
| `Export-PowerViewCSV`               | Append results to a CSV file                                                               |
| `ConvertTo-SID`                     | Convert a User or group name to its SID value                                              |
| `Get-DomainSPNTicket`               | Requests the Kerberos ticket for a specified Service Principal Name (SPN) account          |
| **Domain/LDAP Functions:**          |                                                                                            |
| `Get-Domain`                        | Will return the AD object for the current (or specified) domain                            |
| `Get-DomainController`              | Return a list of the Domain Controllers for the specified domain                           |
| `Get-DomainUser`                    | Will return all users or specific user objects in AD                                       |
| `Get-DomainComputer`                | Will return all computers or specific computer objects in AD                               |
| `Get-DomainGroup`                   | Will return all groups or specific group objects in AD                                     |
| `Get-DomainOU`                      | Search for all or specific OU objects in AD                                                |
| `Find-InterestingDomainAcl`         | Finds object ACLs in the domain with modification rights set to non-built in objects       |
| `Get-DomainGroupMember`             | Will return the members of a specific domain group                                         |
| `Get-DomainFileServer`              | Returns a list of servers likely functioning as file servers                               |
| `Get-DomainDFSShare`                | Returns a list of all distributed file systems for the current (or specified) domain       |
| **GPO Functions:**                  |                                                                                            |
| `Get-DomainGPO`                     | Will return all GPOs or specific GPO objects in AD                                         |
| `Get-DomainPolicy`                  | Returns the default domain policy or the domain controller policy for the current domain   |
| **Computer Enumeration Functions:** |                                                                                            |
| `Get-NetLocalGroup`                 | Enumerates local groups on the local or a remote machine                                   |
| `Get-NetLocalGroupMember`           | Enumerates members of a specific local group                                               |
| `Get-NetShare`                      | Returns open shares on the local (or a remote) machine                                     |
| `Get-NetSession`                    | Will return session information for the local (or a remote) machine                        |
| `Test-AdminAccess`                  | Tests if the current user has administrative access to the local (or a remote) machine     |
| **Threaded 'Meta'-Functions:**      |                                                                                            |
| `Find-DomainUserLocation`           | Finds machines where specific users are logged in                                          |
| `Find-DomainShare`                  | Finds reachable shares on domain machines                                                  |
| `Find-InterestingDomainShareFile`   | Searches for files matching specific criteria on readable shares in the domain             |
| `Find-LocalAdminAccess`             | Find machines on the local domain where the current user has local administrator access    |
| **Domain Trust Functions:**         |                                                                                            |
| `Get-DomainTrust`                   | Returns domain trusts for the current domain or a specified domain                         |
| `Get-ForestTrust`                   | Returns all forest trusts for the current forest or a specified forest                     |
| `Get-DomainForeignUser`             | Enumerates users who are in groups outside of the user's domain                            |
| `Get-DomainForeignGroupMember`      | Enumerates groups with users outside of the group's domain and returns each foreign member |
| `Get-DomainTrustMapping`            | Will enumerate all trusts for the current domain and any others seen.                      |
