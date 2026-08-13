DNS resolve computer names into IP addresses, and it does not have a central database.

#### Types of DNS:
1. DNS root server
	The root servers of the DNS are responsible for the top-level domains
2. Authoritative name server
	Authoritative name servers hold authority for a particular zone.
3. Non-authoritative server
	Non-authoritative name servers are not responsible for a particular DNS zone.
4. Caching server
	It cache information from other name servers for a specified period.
5. Forwarding server
	They forward DNS queries to another DNS server.
6. Resolver
	It perform name resolution locally in the computer or router.

NOTE: DNS also stores and outputs additional information about the services associated with a domain.


| **DNS Record** | **Description**                                                                                                                                                                                                                                                                             |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A              | Returns an IPv4 address of the requested domain as a result.                                                                                                                                                                                                                                |
| AAAA           | Returns an IPv6 address of the requested domain.                                                                                                                                                                                                                                            |
| MX             | Returns the responsible mail servers as a result.                                                                                                                                                                                                                                           |
| NS             | Returns the DNS servers (nameservers) of the domain.                                                                                                                                                                                                                                        |
| TXT            | This record can contain various information. The all-rounder can be used, e.g., to validate the Google Search Console or validate SSL certificates. In addition, SPF and DMARC entries are set to validate mail traffic and protect it from spam.                                           |
| CNAME          | This record serves as an alias for another domain name. If you want the domain [www.hackthebox.eu](http://www.hackthebox.eu) to point to the same IP as hackthebox.eu, you would create an A record for hackthebox.eu and a CNAME record for [www.hackthebox.eu](http://www.hackthebox.eu). |
| PTR            | The PTR record works the other way around (reverse lookup). It converts IP addresses into valid domain names.                                                                                                                                                                               |
| SOA            | Provides information about the corresponding DNS zone and email address of the administrative contact.                                                                                                                                                                                      |
