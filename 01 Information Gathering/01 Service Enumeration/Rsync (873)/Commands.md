[Rsync](https://linux.die.net/man/1/rsync) is a fast and efficient tool for locally and remotely copying files. It can be used to copy files locally on a given machine and to/from remote hosts. It is highly versatile and well-known for its delta-transfer algorithm

# Nmap scan
```
sudo nmap -sV -p 873 "$ip"
```
#### List shares
```
nc -nv "$ip" 873
>> list
```
# Enumeration
```
rsync -av --list-only rsync://"$ip"/share
```

