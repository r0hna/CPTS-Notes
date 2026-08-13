#externalrecon 
# Tools
- `Pre2k` - A tool for pre-windows 2000 compatibility enumeration (use p2k to find users with weak passwords)
- `BloodyAD` - Active directory enumeration and exploitation tool
- `Kerbrute` - A Kerberos brute-force tool
- `Ensurepath` - A tool for managing python-based applications

# Engagement - What we are looking for?
| **Data Point**       | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `IP Space`           | Valid ASN for our target, netblocks in use for the organization's public-facing infrastructure, cloud presence and the hosting providers, DNS record entries, etc.                                                                                                                                                                                                                                                                                |
| `Domain Information` | Based on IP data, DNS, and site registrations. Who administers the domain? Are there any subdomains tied to our target? Are there any publicly accessible domain services present? (Mailservers, DNS, Websites, VPN portals, etc.) Can we determine what kind of defenses are in place? (SIEM, AV, IPS/IDS in use, etc.)                                                                                                                          |
| `Schema Format`      | Can we discover the organization's email accounts, AD usernames, and even password policies? Anything that will give us information we can use to build a valid username list to test external-facing services for password spraying, credential stuffing, brute forcing, etc.                                                                                                                                                                    |
| `Data Disclosures`   | For data disclosures we will be looking for publicly accessible files ( `.pdf, .ppt, .docx, .xlsx`, etc. ) for any information that helps shed light on the target. For example, any published files that contain `intranet` site listings, user metadata, shares, or other critical software or hardware in the environment (credentials pushed to a public GitHub repo, the internal AD username format in the metadata of a PDF, for example.) |
| `Breach Data`        | Any publicly released usernames, passwords, or other critical information that can help an attacker gain a foothold.                                                                                                                                                                                                                                                                                                                              |

- IP Space - ASN/IP registers 
	- [IANA](https://www.iana.org/), [arin](https://www.arin.net/) for searching the Americas, [RIPE](https://www.ripe.net/) for searching in Europe, [BGP Toolkit](https://bgp.he.net/) 

- Domain registration & DNS 
	- [Domaintools](https://www.domaintools.com/), [PTRArchive](http://ptrarchive.com/), [ICANN](https://lookup.icann.org/lookup), manual DNS record requests against the domain in question or against well known DNS servers, such as 8.8.8.8. 

- Social media 
	- Searching LinkedIn, Twitter, Facebook, your region's major social media sites, news articles, and any relevant info you can find about the organization. 

- Public-facing company website 
	- Often, the public website for a corporation will have relevant info embedded. News articles, embedded documents, and the "About Us" and "Contact Us" pages can also be gold mines. 

- Cloud  & Dev storage space 
	- [GitHub](https://github.com/), [AWS S3 buckets & Azure Blog storage containers](https://grayhatwarfare.com/), [Google searches using "Dorks"](https://www.exploit-db.com/google-hacking-database) 

- Breach data sources 
	- [HaveIBeenPwned](https://haveibeenpwned.com/) to determine if any corporate email accounts appear in public breach data, [Dehashed](https://www.dehashed.com/) to search for corporate emails with cleartext passwords or hashes we can try to crack offline. We can then try these passwords against any exposed login portals (Citrix, RDS, OWA, 0365, VPN, VMware Horizon, custom applications, etc.) that may use AD  

# DNS Information
- [whois.domaintools.com](https://whois.domaintools.com/) 
- [viewdns.info](https://viewdns.info/) 
- `nslookup <name server>`
# Public data (job posts)
- LinkedIn 
- Indeed
- Glassdoor 
- Tools 
	- [Trufflehog](https://github.com/trufflesecurity/truffleHog) and sites like [Greyhat Warfare](https://buckets.grayhatwarfare.com/) are fantastic resources. 
	- For a more detailed introduction to OSINT and external enumeration, check out the [Footprinting](https://academy.hackthebox.com/course/preview/footprinting) and [OSINT:Corporate Recon](https://academy.hackthebox.com/course/preview/osint-corporate-recon) modules. 
# Other resource 
- Company website 
- Github 
- Cloud storage 
- [https://github.com/trufflesecurity/truffleHog](https://github.com/trufflesecurity/truffleHog) 
- [https://buckets.grayhatwarfare.com/](https://buckets.grayhatwarfare.com/) 

# Over-searching enumeration principles
- Keep in mind that our goal is to understand our target better. We are looking for every possible venue. First we will use passive resource, and then active enumeration. 

# Google dorks 
```
inurl:inlanefreight.com filetype:pdf
```
```
intext:"@inlanefreight.com" inurl:inlanefreight.com
```
```
"Contact us" page of company website
```
# Username harvesting 
#### [linkedin2username](https://github.com/initstring/linkedin2username) 
#### Credentials hunting (breach data):
##### [dehashed.com](http://dehashed.com/) 
```
sudo python3 dehashed.py -q inlanefreight.local -p
```
##### [dehashed.py](https://github.com/mrb3n813/Pentest-stuff/blob/master/dehashed.py) OR [dehashed.py](https://github.com/sm00v/Dehashed)

---
# Theory
#### Detailed user enumeration - build a user list
A computer object is treated as a domain user account (with some differences, such as authenticating across forest trusts). If you don’t have a valid domain account, and SMB NULL sessions and LDAP anonymous binds are not possible, you can create a user list using external resources such as email harvesting and LinkedIn.

