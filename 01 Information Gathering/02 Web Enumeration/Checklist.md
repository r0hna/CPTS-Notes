# Web Application Enumeration Checklist (CPTS-Aligned)

## Reconnaissance & Information Gathering
- [ ] Subdomain enumeration  
  `sublist3r -d example.com`  
  `amass enum -d example.com`  
  `dig example.com any`
- [ ] DNS zone transfer  
  `dig AXFR example.com @ns1.example.com`
- [ ] WHOIS domain lookup  
  `whois example.com`
- [ ] Metadata extraction from public files  
  `exiftool file.pdf`
- [ ] `robots.txt` file check 
- [ ] Search public sources & OSINT for endpoints and creds  

## Technology & Fingerprinting
- [ ] Identify web server/version  
  `curl -I http://example.com` (Look for Server header)
- [ ] Detect web framework/CMS/plugins  
  Use Wappalyzer browser extension or  
  `whatweb http://example.com`
- [ ] Inspect HTTP headers/cookies for security flags  
  `curl -I http://example.com` and analyze Set-Cookie flags

## Directory & File Enumeration
- [ ] Directory brute force  
  `gobuster dir -u http://example.com -w wordlist.txt`
- [ ] Check for common files:  
  `curl http://example.com/robots.txt`  
  `curl http://example.com/sitemap.xml`  
  `curl http://example.com/.git/config`
- [ ] Look for backup or sensitive files  
  Use wordlists with extensions like `.bak`, `.old`, `.zip`

## Input Points & Attack Surfaces
- [ ] List all form fields and parameters (manual or Burp Suite)
- [ ] Identify supported HTTP methods  
  `curl -X OPTIONS http://example.com -i`
- [ ] Check authentication/login pages, API endpoints

## Vulnerability Testing
- Broken Authentication  
  - Test default weak creds  
  - Password reset workflows
- Injection Flaws  
  - Use SQLMap example:  
	`sqlmap -u "[http://example.com/vuln.php?id=1](http://example.com/vuln.php?id=1)" --batch --dbs`
- Cross-Site Scripting (XSS)  
- Manual payloads and Burp Scanner
- File Inclusion/Upload  
- Test for LFI/RFI and unrestricted upload paths
- Server-Side Request Forgery (SSRF) and Template Injection (SSTI)  

## Security Misconfiguration & Access Control
- [ ] Directory listing enabled?  
Browsing to directories without index pages
- [ ] Misconfigured CORS, HTTP methods
- [ ] Broken access control (IDOR tests)
- [ ] Horizontal and vertical privilege escalation tests

## Error Handling & Information Disclosure
- [ ] Inject invalid inputs to observe error messages  
- [ ] Look for stack traces and debug info in responses

## Session Management
- [ ] Check cookie flags `HttpOnly`, `Secure`
- [ ] Test session fixation and logout functions

## Tools & Automation
- Burp Suite for proxying and automated scans
- Nikto for web server vuln detection  
`nikto -h http://example.com`
- Gobuster or ffuf for fuzzing URLs and files  
- SQLMap for SQL injection automation

---

**Documentation:** Save URLs, requests, responses, payloads, and screenshots for reporting in the CPTS exam.

