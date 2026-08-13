# Enumerate the remote desktop users group
#winrmuser #winrmgroup #winrmusergroup #remotedesktopuser
```
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Desktop Users"
```
# Check domain user group local admin & execution rights (Bloodhound) 
```
Node info tab > Execution rights section > first degree RDP privileges
```
# Find workstations/servers where domain users can RDP 
```
Analysis Tab
```
# Win-rm access users
#winrmuser #winrmgroup #winrmaccess
>Enumerate the Remote Management users group
#### Built-In tool 
```
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Management Users"
```
#### Bloodhound
#customquery #bloodhoundquery
>winrm access via bloodhound query
```
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:CanPSRemote*1..]->(c:Computer) RETURN p2
```

>Check for SQL admin rights
```
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:SQLAdmin*1..]->(c:Computer) RETURN p2
```

#bloodhoundcustomquery
>[Bloodhound cipher query cheatsheet](https://hausec.com/2019/09/09/bloodhound-cypher-cheatsheet/)