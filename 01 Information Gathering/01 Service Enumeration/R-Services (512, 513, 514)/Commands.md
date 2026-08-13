### R-services
*R-Services are a suite of services hosted to enable remote access or issue commands between Unix hosts over TCP/IP. Initially developed by the Computer Systems Research Group (CSRG) at the University of California, Berkeley,r-serviceswere the de facto standard for remote access between Unix operating systems until they were replaced by the Secure Shell (SSH) protocols and commands due to inherent security flaws built into them.*

# Nmap scan
```
sudo nmap -sV -p 512,513,514 "$ip"
```
#### Login
```
rlogin "$ip" -l htb-student
```
#### Listing authenticated users
```
rwho
rusers -al "$ip"
```


#### The [R-commands](https://en.wikipedia.org/wiki/Berkeley_r-commands) suite consists of the following programs:
- rcp (`remote copy`)
- rexec (`remote execution`)
- rlogin (`remote login`)
- rsh (`remote shell`)
- rstat
- ruptime
- rwho (`remote who`)