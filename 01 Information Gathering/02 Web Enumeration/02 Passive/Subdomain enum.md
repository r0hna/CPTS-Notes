>HTB: https://academy.hackthebox.com/module/144/section/1258
# Resource to discover subdomains
1. Certificate Transparency logs
```
curl -s "https://crt.sh/?q=$domain&output=json" | jq -r '.[]
 | select(.name_value | contains("dev")) | .name_value' | sort -u
```
1. Public repositories of SSL/TLS certificates.
2. Utilizing search engine like google, DuckDuckGo
3. Dark web search engine and web forms