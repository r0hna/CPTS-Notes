# Open Replay
```
mynetworks = 0.0.0.0/0

#With this setting, this SMTP server can send fake emails and thus initialize communication b/w multiple parties. Another attack would be to spoof the email and read it.
```

# nmap - open relay attack
```
sudo nmap "$ip" -p25 --script smtp-open-relay -v
```