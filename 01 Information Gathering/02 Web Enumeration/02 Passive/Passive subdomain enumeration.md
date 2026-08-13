# WHOIS
```
whois doamin.com
```
#### WHOIS: Phishing investigation
The whois record reveals the following:
1. *Registration date*:- The domain was registered just a few day ago.
2. *Registrant*:- The registrant's information is hidden behind a privacy service.
3. *Name servers*:- The name server are associated with a known bulletproof hosting provider often used for malicious activities.

#### WHOIS: Malware analysis
The WHOIS record reveals:
1. *Registrant*: The domain is registered to an individual using a free email service known as anonymity.
2. *Location*: The registrant's address is in a country with a high prevalence of cyber-crime.
3. *Registrar*: The domain was registered through a registrar with a history of lax abuse policies.

#### WHOIS: Threat intelligence report
Analysis uncover the following patterns:
1. *Registration Dates*: The domains were registered in clusters, often shortly before major attacks.
2. *Registrants*: The registrants use various aliases and fake identities.
3. *Name Servers*: The domains often share the same name servers, suggesting a common infrastructure.
4. *Takedown History*: Many domains have been taken down after attacks, indicating previous law enforcement or security interventions.



## DNS information
- [https://domain.glass](https://domain.glass)
- `dig any "$domain"`
## Cloud information gather
- [Grayhatwarfare](https://grayhatwarfare.com/)
## Websites to enumerate subdomains
- [https://crt.sh](https://crt.sh)
- [https://ui.ctsearch.entrust.com/ui/ctsearchui](https://ui.ctsearch.entrust.com/ui/ctsearchui)
- certspotter
- dnscan
- amass
## Filter out the result
```
curl -s https://crt.sh/?q\="$domain"\&output\=json | jq ".[].common_name,.[].name_value"| cut -d'"' -f2 | sed 's/\\n/\n/g' | sed 's/\*.//g'| sed -r 's/([A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4})//g' | sort -u
```
### Domain to IP
```
For i in $(cat subdomain.list);do host $i|grep "has address"|grep "$domain" |cut -d" "-f1,4;done
```
### SHODAN search
`for i in $(catip-addresses.txt);do shodan host $i; done`

>NOTE: Identify which software/technologies are used by companies (Record TXT)




