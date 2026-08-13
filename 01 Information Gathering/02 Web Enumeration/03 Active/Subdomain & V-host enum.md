**Sub-domain vs v-host:**
The key difference between Vhost and sub-domains is that a Vhost is basically a 'sub-domain' served on the same server and has the same IP, such that a single IP could be serving two or more different websites.
#### Wordlists (DNS)
```
/usr/share/SecLists/Discovery/DNS/namelist.txt
/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-110000.txt
/usr/share/seclists/Discovery/DNS/fierce-hostlist.txt
```

# Sub-domain enumeration
#### Manual script (dig)
```
for sub in $(cat /usr/share/SecLists/Discovery/DNS/subdomains-top1million-110000.txt);do dig "$domain" @"$ip" |grep -v ';\|SOA'|sed -r '/^\s*$/d'|grep $sub|tee -a subdomains_dig.txt;done
```
#### FFUF
```
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u https://FUZZ.inlanefreight.com/
```
#### Gobuster
```
gobuster dns --do "$domain" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --resolver "$ip" --ne
```
#### DNS-enum
```
dnsenum --dnsserver "$ip" --enum -o subdomains_dnsenum.txt -f /usr/share/seclists/Discovery/DNS/fierce-hostlist.txt --threads 90 "$domain" #-p 0 -s 0
```

---
# Vhost enumeration
#### Gobuster
```
gobuster vhost -u http://"$domain":53 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt -t 25 --append-domain -o vhost_"$ip"_gobuster.out
```
#### FFUF
```
ffuf -u http://"$ip/" -H "Host: FUZZ.$domain" -mc all -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -t 80 -o vhost_"$ip"_ffuf.out
```
								OR
```
ffuf -c -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb'
```
