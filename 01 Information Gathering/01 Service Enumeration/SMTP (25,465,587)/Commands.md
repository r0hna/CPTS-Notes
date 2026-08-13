# Nmap scan
```
sudo nmap -Pn -sV -sC -p25,143,110,465,587,993,995 --script=smtp* -p 25 "$ip"
```
# Interact with the SMTP server
```
telnet "$ip" 25
nc "$ip" 25


## Commands
>> HELO mail1.domain.com
```
# Send mail
```
swaks --to itsupport@"$domain" --from marmeus@marmeus.com --server "$domain" --body "http://10.10.16.16/"
```
# User enum
```
smtp-user-enum -M VRFY -U /usr/share/wordlists/metasploit/unix_users.txt -t "$ip"
```


