# DNS queries
#### Version query
```
dig CH TXT version.bind "$ip"
```
#### Check DNS entry of a domain
```
dig +noall +answer @"$ip" "$domain" any
```
#### DNS record (any)
```
dig any "$domain" @"$ip"
```
#### NS query
```
dig ns "$domain"
```
#### Reverse DNS lookup
```
dig -x <target> @1.1.1.1
```

# Zone Transfer check
>User domain name, instead of IP address
```
dig axfr @"$ip" "$sub.domain"
```
```
dig @trilocor.local trilocor.local axfr
```
					AND
```
dig soa "$domain"
```


## Test
```
dig axfr @nsztm1.digi.ninja zonetransfer.me
```
