# Footprint
```
sudo nmap -sV -p- --open -T4 10.129.201.50
```

# Identify version
```
curl -s http://10.129.201.50:8080/index.htm -A "Mozilla/5.0 (compatible;  MSIE 7.01; Windows NT 5.0)" | grep version
```

# Gain access to web application
- Use default credentials