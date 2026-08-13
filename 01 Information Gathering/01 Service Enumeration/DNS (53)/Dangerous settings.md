#### Bind 9 [CVE details](https://www.cvedetails.com/product/144/ISC-Bind.html?vendor_id=64)
# DNS attacks
[Popular type of DNS attacks](https://web.archive.org/web/20250329174745/https://securitytrails.com/blog/most-popular-types-dns-attacks)

# Most common
1. **Incorrect DNS Records:** Mistyped or outdated records can lead to service disruptions or unintentional traffic redirection.
2. **Open DNS Resolvers:** Leaving DNS resolvers open to the public can enable attackers to use them for Distributed Denial of Service (DDoS) amplification attacks.
3. **Lack of DNSSEC Implementation:** Failing to implement DNS Security Extensions (DNSSEC) leaves the system vulnerable to cache poisoning and spoofing attacks.
4. **Improper Forwarding Configurations:** Misconfigured DNS forwarding can expose sensitive queries to unauthorized parties.

# Dangerous entries

| **Option**        | **Description**                                                                |
| ----------------- | ------------------------------------------------------------------------------ |
| `allow-query`     | Defines which hosts are allowed to send requests to the DNS server.            |
| `allow-recursion` | Defines which hosts are allowed to send recursive requests to the DNS server.  |
| `allow-transfer`  | Defines which hosts are allowed to receive zone transfers from the DNS server. |
| `zone-statistics` | Collects statistical data of zones.                                            |
