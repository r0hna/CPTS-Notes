### 🌐 Web Enumeration

The CPTS exam is packed with web interfaces — some internal, some custom, many deceptive. Learning to **approach them methodically** and understand their logic is crucial.

🔎 **Active Web Recon  
*These are the noisy techniques — but essential when used surgically.*

- **Directory and Page Fuzzing**: Tools like `ffuf`, `dirsearch`, or `feroxbuster` with custom and general wordlists (SecLists, robots.txt leaks, known paths from CMSs)
- **Parameter and Value Fuzzing**: Great for discovering hidden GET/POST parameters, testing auth logic or finding vulnerable paths like `debug=true`.
- **VHost Discovery**: Using tools like `ffuf -H "Host: FUZZ.target"` with known DNS entries or certificate parsing
- **Header Analysis**: Look at cookies, server headers, CORS policies, cache behavior

🛡️ **Passive Web Recon  
**Sometimes the best enumeration is silent. Use passive tools **before** active fuzzing, especially when assessing exposed services.

- **Google Dorks**: Leak detection, repo finds, forgotten staging apps
- **Technology Stack Analysis**: Tools like `wappalyzer`, `whatweb`, `builtwith`, or headers via Burp/HTTPx
- **DNS and Certificate Recon**: Using tools like `crt.sh`, `amass`, `certspotter`, or `dnscan` to fingerprint internal infra

**Tools You Should Know Well:**

- `FinalRecon`: Swiss-army knife for passive recon
- `Spiderfoot`: Automated passive OSINT (note: requires tweaking to avoid noise)
- `Recon-ng`: Good for linked enumeration and correlating data
- `theHarvester`: Simple but great for emails and DNS records
- `Eyewitness`: Captures screenshots of web portals across subdomains — great for internal pivot recon
- **OSINT Framework**: Reference chart to explore passive enumeration targets

### 🧱 Application Fingerprinting

Throughout the CPTS exam, you’ll encounter real-world applications: enterprise tools, CMSs, ticketing systems, or internal dashboards. The key is **recognizing them fast** and checking for known attack surfaces — but also understanding that sometimes the flaws are logic-based, not CVE-based.

**Recognizable Apps You Should Be Able to Enumerate and Attack**:

- **CMSs**: WordPress, Joomla, Drupal, DotNetNuke
- **DevOps**: Jenkins, GitLab
- **Monitoring**: PRTG Network Monitor, Nagios XI, Splunk
- **Web Servers**: Apache Tomcat, ColdFusion, WebSphere, WebLogic, Axis2
- **Ticketing Systems**: osTicket (especially common), internal CRMs or dashboards

🧠 What you need is not just CVE knowledge, but the ability to recognize:

- Default credentials or misconfigurations
- Hidden admin portals (`/admin`, `/manage`, `/super`)
- Debug or backup endpoints (`.bak`, `/debug`, `?stage=`)

If you’re treating every web app like an FFUF target, you’re missing the bigger picture. You need to start **walking the app manually** and watching how it handles user state, access control, and misbehavior.