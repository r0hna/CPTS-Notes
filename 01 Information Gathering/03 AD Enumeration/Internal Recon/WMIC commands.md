>Useful commands Cheat sheet  - [xorrior - 67ee741af08cb1fc86511047550cdaf4](https://gist.github.com/xorrior/67ee741af08cb1fc86511047550cdaf4) 
#### Print patch level and `hostfixes` 
```
wmic qfe get Caption,Description,HotFixID,InstalledOn
```
#### Display basic host information 
```
wmic computersystem get Name,Domain,Manufacturer,Model,Username,Roles /format:List
```
#### List all process 
```
wmic process list /format:list
```
#### Print domain and Domain Controller information 
```
wmic ntdomain list /format:list
```
#### Print all local and domain accounts 
```
wmic useraccount list /format:list
```
#### local groups 
```
wmic group list /format:list
```
#### Any system account that are being used as service accounts
```
wmci sysaccount list /format:list
```
#### Print domain, child-domain, and forest trust 
```
wmic ntdomain get Caption,Description,DnsForestName,DomainName,DomainControllerAddress
```

# Net commands

| Command                                       | Description                                                                                                                |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| net accounts                                  | Information about password requirements                                                                                    |
| net accounts /domain                          | Password and lockout policy                                                                                                |
| net group /domain                             | Information about domain groups                                                                                            |
| net group "Domain Admins" /domain             | List users with domain admin privileges                                                                                    |
| net group "domain computers" /domain          | List of PCs connected to the domain                                                                                        |
| net group "Domain Controllers" /domain        | List PC accounts of domains controllers                                                                                    |
| net group <domain_group_name> /domain         | User that belongs to the group                                                                                             |
| net groups /domain                            | List of domain groups                                                                                                      |
| net localgroup                                | All available groups                                                                                                       |
| net localgroup administrator                  | Users that belonged to administrator group                                                                                 |
| net localgroup administrators /domain         | List users that belong to the administrators group inside the domain (the group Domain Admins is included here by default) |
| net localgroup Administrators                 | Information about a group (admins)                                                                                         |
| net localgroup administrators [username] /add | Add user to administrators                                                                                                 |
| net share                                     | Check current shares                                                                                                       |
| net user <ACCOUNT_NAME> /domain               | Get information about a user within the domain                                                                             |
| net user /domain                              | List all users of the domain                                                                                               |
| net user /domain user                         | Information about domain user                                                                                              |
| net user %username%                           | Information about the current user                                                                                         |
| net use x: \computer\share                    | Mount the share locally                                                                                                    |
| net view                                      | Get a list of computers                                                                                                    |
| net view /all /domain[:domainname]            | Shares on the domains                                                                                                      |
| `net view \\computerName /ALL`                | List shares of a computer                                                                                                  |
| net share                                     |                                                                                                                            |
| net view /domain                              | List of PCs of the domain                                                                                                  |
| net1                                          | Use net1 instead of net to avoid logging                                                                                   |
