# Check for `CanPSRemote` rights
>Bloodhound custom query) #customquery
```
MATCH p1=shortestPath((u1:User)-[r1:MemberOf*1..]->(g1:Group)) MATCH p2=(u1)-[:CanPSRemote*1..]->(c:Computer) RETURN p2
```

# Establish Win-rm session 
#### Windows 
```
$password = ConvertTo-SecureString "Klmcargo2" -AsPlainText -Force
```
```
$cred = new-object System.Management.Automation.PSCredential ("INLANEFREIGHT\forend", $password)
```
```
Enter-PSSession -ComputerName ACADEMY-EA-MS01 -Credential $cred
```
#### Linux 
```
gem install evil-winrm
```
```
evil-winrm -I 10.129.201.234 -u forend
```

