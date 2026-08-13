#### Get domain info
```
Get-ADDomain
```
#### Enumerating trust relation
>Built-in tool
```
Import-Module activedirectory
Get-ADTrust -Filter *
```
#### Check for existing trust relation (power-view)
```
Get-DomainTrust
```
#### Domain trust mapping (type & direction of trust)
```
Get-DomainTrustMapping
```
#### Checking users in the child domain
```
Get-DomainUser -Domain LOGISTICS.INLANEFREIGHT.LOCAL | select SamAccountName
```
#### Test for local admin access (current user)
```
Test-AdminAccess -ComputerName ACADEMY-EA-MS01
```

---
### Another tool we can use is `netdom`
#### Query domain trust
```
netdom query /domain:inlanefreight.local trust
```
#### Query DC
```
netdom query /domain:inlanefreight.local dc
```
#### Query server and workstations
```
netdom query /domain:inlanefreight.local workstation
```
