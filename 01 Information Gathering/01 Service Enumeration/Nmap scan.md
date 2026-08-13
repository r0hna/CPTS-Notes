>Do individual port's nmap scripts scan - `--script vuln,smb,....`
>Understand ports in depth - `--packet-trace --reason`
# Host discovery
```
sudo nmap -sn "$ip" -oN scan/live_hosts.out -n -PE --disable-arp-ping | grep for | cut -d" " -f5
```
					OR
>Using more than one probe to detect more hosts/ports
```
sudo nmap -sn -oN scan/live_hosts.out -n -PE -PP -T4 --source-port 53 "$ip" --disable-arp-ping | grep for | cut -d" " -f5
```
```
sudo nmap -sn "$ip" -oN scan/live_hosts.out -n -PE -PP -p80,443,113 -PA80,113,443,10042 -T4 --source-port 53 "$ip" --disable-arp-ping | grep for | cut -d" " -f5
```
# UDP Scan (top 100)
```
sudo nmap "$ip" -F -sU -sS -n --disable-arp-ping -oN scan/udp_scan"$ip".nmap
```
# TCP Scan
```
sudo nmap "$ip" -p- -n --disable-arp-ping -oN scan/nmap-tcp_quick"$ip".nmap
```
```
sudo nmap "$ip" -p"$ports" -sVC -Pn -A --script version,banner,safe -n --disable-arp-ping -oN scan/nmap-tcp-full"$ip".nmap -oX scan/nmap-tcp-full"$ip".xml
```
#### Grep Nmap port
#grep #grepnmap #grepnmapresult
```
grep '^53\|^21\|^143\|^993\|^632\|^88\|^1433\|^1434\|^2433\|^3306\|^111\|^2049\|^1521\|^110\|^995\|^512\|^513\|^514\|^3389\|^873\|^139\|^445\|^25\|^465\|^D587\|^161\|^162\|^10161\|^10162\|^22\|^69\|^80'
```
# Web-ports only
```
nmap -p 80,443,8080,8443,8181,8000,8888 --open -oN scan/web_discovery_"$ip".nmap
```
# xml to html
```
xsltproc target.xml -o target.html
```

---

>Analysis the web headers or error web page to know about the technology. 
# Firewall and IDS-IPS evasion
>look out for great [nmap scan strategies](https://nmap.org/book/host-discovery-strategies.html)
1. `-f --mtu 512` - Fragment packets into smaller 512 bytes.
2. Using a DNS source port - `-sS -Pn -n --disable-arp-ping --packet-trace --source-port 53` (No hosts disable/block DNS query, even WAF)
3. Using decoy flag - `-D RND:5`
4. Using more than one probe to detect hosts - `nmap -n -sn -PE -PP -p80,443,113 -PA80,113,443,10042 -T4 --source-port 53 "$ip"`
5. using `ACK flag`- `nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace`

---
# Automation
```
sudo autorecon "$ip" --scan.domain "$domain"
```
# One-Line Scan
```
export ports=$(sudo nmap -p- --min-rate=900 "$ip" | grep '^[0-9]' | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//) && (mkdir scan 2>/dev/null || ls -ld scan) && sudo nmap -p$(echo $ports | tr '\n' ',') -sVC "$ip" --script "banner and safe and not brute and not broadcast and not vulners and not http-comments-displayer and not multicast-profinet-discovery and not *-robtex* and not targets-asn" -oA scan/scan_"$ip"
```
					OR
```
export ports=$(sudo nmap -p- --min-rate=900 "$ip" | awk '/^[0-9]+\/open/ {print $1}' | cut -d '/' -f 1 | paste -sd ',' -) && \
[ -n "$ports" ] && (mkdir -p scan && sudo nmap -p"$ports" -sVC "$ip" \
--script "banner and safe and not brute and not broadcast and not vulners and not http-comments-displayer and not multicast-profinet-discovery and not *-robtex* and not targets-asn" \
-oN scan/scan_"$ip".nmap) || echo "[!] No open ports found on $ip"
```
#### `.zshrc` function
```
scan() {
  if [ -z "$ip" ]; then
    echo "[!] IP not set. Use: export ip=192.168.x.x"
    return 1
  fi

  echo "[*] Scanning all ports on $ip..."
  export ports=$(sudo nmap -p- --min-rate=900 "$ip" | awk '/^[0-9]+\/open/ {print $1}' | cut -d '/' -f 1 | paste -sd ',' -)

  if [ -n "$ports" ]; then
    echo "[+] Open ports: $ports"
    mkdir -p scan
    sudo nmap -p"$ports" -sVC "$ip" \
      --script "safe and not brute and not broadcast and not vulners and not http-comments-displayer and not multicast-profinet-discovery and not *-robtex* and not targets-asn" \
      -oN scan/scan_"$ip".nmap
    echo "[✓] Scan saved to scan/scan_$ip.nmap"
  else
    echo "[!] No open ports found on $ip"
  fi
}
```


# Nmap script engine
|**Category**|**Description**|
|---|---|
|`auth`|Determination of authentication credentials.|
|`broadcast`|Scripts, which are used for host discovery by broadcasting and the discovered hosts, can be automatically added to the remaining scans.|
|`brute`|Executes scripts that try to log in to the respective service by brute-forcing with credentials.|
|`default`|Default scripts executed by using the `-sC` option.|
|`discovery`|Evaluation of accessible services.|
|`dos`|These scripts are used to check services for denial of service vulnerabilities and are used less as it harms the services.|
|`exploit`|This category of scripts tries to exploit known vulnerabilities for the scanned port.|
|`external`|Scripts that use external services for further processing.|
|`fuzzer`|This uses scripts to identify vulnerabilities and unexpected packet handling by sending different fields, which can take much time.|
|`intrusive`|Intrusive scripts that could negatively affect the target system.|
|`malware`|Checks if some malware infects the target system.|
|`safe`|Defensive scripts that do not perform intrusive and destructive access.|
|`version`|Extension for service detection.|
|`vuln`|Identification of specific vulnerabilities.|