### Hunt Company Staff
- LinkedIn or Xing (Check out the employee)
- Search for the job posting or current employs by the company.
- GitHub repositories
- Current employee profiles.
- Check out the language preferences/skill and etc.
- Try to find code/github repo which lead to technology.

Companies always hire employees whose skills they can use and apply to the business. For example, we know that Flask and Django are web frameworks for the Python programming language.

If we do a little search for Django security misconfigurations, we will eventually come across the following [Github repository](https://github.com/boomcamp/django-security) that describes OWASP Top10 for Django. We can use this to understand the inner structure of Django and how it works.

#### Tech detection
- `wappalyzer`
- `whatweb`
- `builtwith`
- HTTP header

---
# Infrastructure based enumeration
#### Certificate #subdoamin
```
curl -s "https://crt.sh/\?q\=$domain\&output\=json" | jq .
```
*Filter out the result*
```
 curl -s "https://crt.sh/\?q\=$domain\&output\=json" | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```
#### Use shodan
```
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done && for i in $(cat ip-addresses.txt);do shodan host $i;done
```
#### DNS record
```
dig any "$domain"
```
#### Google dork
```
intext:passwd inurl:amazonaws.com
intext:google inurl:blob.core.windows.net
```
#### Target website source code
```
Press CTRL + U
```
#### Domain.Glass Results
```
https://domain.glass/
```
#### buckets.grayhatwarfare.com
```
Check for things like private or public SSH keys
```