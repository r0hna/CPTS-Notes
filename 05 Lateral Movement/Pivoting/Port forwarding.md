# Metasploit - Port forwarding
```
help portfwd 
```

#### Create local TCP replay 
```
portfwd add -l 3300 -p 3389 -r <third_machine_ip>
```

The above command requests the Meterpreter session to start a listener on our attack host's local port (-l) 3300 and forward all the packets to the remote (-r) Windows server 172.16.5.19 on 3389 port (-p) via our Meterpreter session. Now, if we execute xfreerdp on our localhost:3300, we will be able to create a remote desktop session. 
#### Connecting to windows target through localhost 
```
xfreerdp3 /v:localhost:3300 /u:victor /p:passs@123 /timeout:10000
```
#### Netstat output (port check in windows) 
```
netstat -antp
```

*We can create a reverse port forward on our existing shell from the previous scenario using the below command. This command forwards all connections on port 1234 running on the Ubuntu server to our attack host on local port (-l) 8081. We will also configure our listener to listen on port 8081 for a Windows shell.*

---
# Socat - Port forwarding
- `TCP4-LISTEN:12345,fork` - socat will listen for incoming TCP connections on port 12345 on your local machine. The fork option allows socat to handle multiple connections. 
- `TCP4:10.10.16.16:12345` Once a connection is received, socat will forward it to port 12345 on the remote machine with IP 10.10.16.16. 
```
(nohup ./socat TCP4-LISTEN:12345,fork TCP4:10.10.16.16:12345)&
```
					OR
```
(nohup ./socat TCP-LISTEN:7654,fork TCP:10.10.14.2:1234)&
```
#### One interface to another
```
(nohup ./socat TCP4-LISTEN:8080,fork,reuseaddr TCP4:eth0:9090)&
```
#### Interface binding
```
(nohup ./socat TCP4-LISTEN:445,fork,reuseaddr,bind=172.16.139.10 TCP4:10.10.16.8:445)&
```

---
# Netsh - Port forwarding (Windows)
#windowsportforwarding #portforwardingwindows #portforwarding
#### Using Netsh.exe to port forward 
```
netsh.exe interface portproxy add v4tov4 listenport=8080 listenaddress=<compromised_host> connectport=3389 connectaddress=<third_host_ip>
```
#### Verify port  forward (list forwarded ports)
```
netsh.exe interface portproxy show v4tov4 
```
#### Delete forward port
```
netsh interface portproxy delete v4tov4 listenport=8080 listenaddress=10.10.10.5
```
#### Connect (attacker host) 
```
xfreerdp3 /u:victor /p:pass@123 /v:<compromised_host>:8080 /timeout:10000
```




