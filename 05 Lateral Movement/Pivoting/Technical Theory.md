# DNS tunneling with DNScat2 
Dnscat2 is a tunneling tool that uses DNS protocol to send data between two hosts. It uses an encrypted Command-&-Control (C&C or C2) channel and sends data inside TXT records within the DNS protocol. Usually, every active directory domain environment in a corporate network will have its own DNS server, which will resolve hostnames to IP addresses and route the traffic to external DNS servers participating in the overarching DNS system. However, with dnscat2, the address resolution is requested from an external server. When a local DNS server tries to resolve an address, data is exfiltrated and sent over the network instead of a legitimate DNS request. Dnscat2 can be an extremely stealthy approach to exfiltrate data while evading firewall detections which strip the HTTPS connections and sniff the traffic.

# Socks5 tunneling with chisel 
Chisel is a TCP/UDP-based tunneling tool written in Go that uses HTTP to transport data that is secured using SSH. Chisel can create a client-server tunnel connection in a firewall restricted environment. 

Chisel client run on the attacker (kali) machine and connect to server on the target host, just like SSH. In some cases, kali cannot connect to target on a particular port, so we use reverse connection and set up chisel server on kali and chisel client connect to kali machine.

# ICMP tunneling with socks 
ICMP tunneling encapsulates your traffic within ICMP packets containing echo requests and responses. ICMP tunneling would only work when ping responses are permitted within a firewalled network. When a host within a firewalled network is allowed to ping an external server, it can encapsulate its traffic within the ping echo request and send it to an external server. The external server can validate this traffic and send an appropriate response, which is extremely useful for data exfiltration and creating pivot tunnels to an external server. 

# SocksOverRDP  - RDP and SOCKS tunneling
There are often times during an assessment when we may be limited to a Windows network and may not be able to use SSH for pivoting. We would have to use tools available for Windows operating systems in these cases. [SocksOverRDP](https://github.com/nccgroup/SocksOverRDP) is an example of a tool that uses Dynamic Virtual Channels (DVC) from the Remote Desktop Service feature of Windows. It uses clipboard, audio sharing feature to tunnel arbitrary packets over the network.

We will need to transfer SocksOverRDPx64.zip or just the SocksOverRDP-Server.exe to HOST C. We can then start SocksOverRDP-Server.exe with Admin privileges. 

After that we can transfer the Proxifier portable to windows host and configure it to forward all our packets to 127.0.0.1:1080. Proxifier will route all traffic through the given host and port. 

Walkthrough: [https://academy.hackthebox.com/storage/modules/158/configuringproxifier.gif](https://academy.hackthebox.com/storage/modules/158/configuringproxifier.gif)


# Defensive side 
#### Things to document and track 
- DNS records, network device backups, and DHCP configurations 
- Full and current application inventory 
- A list of all enterprise hosts and their location 
- Users who have elevated permissions 
- A list of any dual-homed hosts (More than one network interface) 
- Keeping a visual network diagram of your environment 
- Tool - [https://www.netbraintech.com/](https://www.netbraintech.com/) 
#### Network hardening categories 
- People 
- Process 
- technology