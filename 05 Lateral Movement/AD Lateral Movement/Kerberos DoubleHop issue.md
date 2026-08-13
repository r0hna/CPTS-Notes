It arises when an *attacker attempts to use Kerberos authentication across two hops*. The issue concerns how Kerberos tickets are granted for specific resources. When we perform Kerberos authentication, we get a 'ticket' that permits us to access the requested resource. On the contrary, when we use password to authenticate, that NTLM hash is stored in our session. A hop/server cannot send forward the user's credentials without special configurations. 

When authentication with Win-rm over two or more connections, the user's passwords is never cached as part of the login.(we won't see credentials in the memory) 
<img src='https://academy.hackthebox.com/storage/modules/143/double_hop.png'/>

# Method 1: PSCredentials Object
Create-credential-object (after connection to the remote host with domain cred - non-joined domain host)

```
Import-module .\PowerView.ps1
klist
```

#### Setup a credentials object
>In evil-winrm session 
```
$SecPassword = ConvertTo-SecureString '!qazXSW@' -AsPlainText -Force
```
```
$Cred = New-Object System.Management.Automation.PSCredential('INLANEFREIGHT\backupadm', $SecPassword)
```
#### Query SPN account 
```
Get-domainuser -spn -credential $cred | select samaccountname
```
```
Klist (check cached tickets)
```
If we RDP to the same host, check tickets using klist via CMD, we have necessary tickets cached. So do not need to worry about the double hop problem because our password is stored in memory, so it can be sent along with query request.

# Method 2: Register PSSession configuration 
#### First establish Win-rm session on the remote host 
>What if we're on a domain-joined host and can connect remotely to another using Win-rm? Or we are working from a Windows attack host.
```
Enter-PSSession -ComputerName ACADEMY-AEN-DEV01.INLANEFREIGHT.LOCAL -Credential inlanefreight\<username>
```
#### Register a PowerShell session config 
```
Register-PSSessionConfiguration -Name session_name -RunAsCredential inlanefreight\<username>
```
#### Restart the WinRM session (In current session) 
```
Restart-Service WinRM
```
#### Reconnect session with PSSession using the named registered session 
```
Enter-PSSession -ComputerName DEV01 -Credential INLANEFREIGHT\backupadm -ConfigurationName  <session_name>
```
#### Run commands
```
get-domainuser -spn | select samaccountname
```



`Register-PSSessionConfiguration` cannot be used by evil-winrm as we won't be able to get the credentials popup. First setup `PSCredential` object and pass the credentials like `-RunAsCredential` $cred, we will get an error because we can only use `RunAs` from an elevated PowerShell terminal. Therefore, this method will not work as it requires GUI access and proper PowerShell console. *This method is still highly effective if we are testing from a Windows attack host and have a set of credentials or compromise a host and can connect via RDP to use it as a "jump host"*

