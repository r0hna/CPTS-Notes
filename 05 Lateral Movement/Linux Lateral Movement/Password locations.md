# Old password locations 
```
sudo cat /etc/security/opasswd
```
# Cracking Linux passwords 
```
sudo cp /etc/passwd /tmp/passwd.bak && sudo cp /etc/shadow /tmp/shadow.bak && unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadow.hashes && echo "File: /tmp/unshadow.hashes"
```
# Cracking hashes 
Md5 hash --- 500
```
hashcat -m 1800 -a 0 /tmp/unshadow.hashes /usr/share/wordlists/rockyou.txt -o cracked.txt
```
