# SSH - Dynamic Port forwarding and SOCKS tunneling
#### SSH - SOCKS tunneling  (multiple ports)  
###### Connect with the compromised host:
```
ssh -D 9050 ubuntu@<compromised_host> 
```
###### In kail machine (attacker box):
Add `socks4 127.0.0.1 9050` to `proxychains.conf`
```
proxychains nmap -v -sn <third_server_ip> 
```

Using nmap with proxychains, it will route all the packets of Nmap to the local port 9050, where our SSH client is listening, which will forward all the packets over SSH to the 172.16.5.0/23 network. *Full TCP connect scan is allowed over proxychains*. 
Host-live checks may not works as ICMP packets are disabled by windows firewall. 

###### How to use proxychains:
```
proxychains msfconsole
```
```
proxychains xfreerdp3
```

---
# Plink - Dynamic port forwarding (windows as attacker host)
#### Using plink
```
plink -ssh -D 9050 ubuntu@<compromised_host_ip>
```
This starts an SSH session between the Windows attack host and the Ubuntu server, and then plink starts listening on port 9050.
#### Another windows based tool
It starts a SOCKS tunnel via the SSH session
```
proxifier.exe
```

*After configuring the SOCKS server for 127.0.0.1 and port 9050, we can directly start mstsc.exe to start an RDP session with a Windows target that allows RDP connections.*

---

