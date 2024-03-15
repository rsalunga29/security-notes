# TODO
Complete this methodology using following as guides: [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web) and [Pentest Book](https://pentestbook.six2dez.com/others/web-checklist).
Create a checklist for each steps.
Create a checklist for each vulnerability types (optional).
## Passive Recon
- Understand the business area and what the customer needs.
- Perform OSINT on the target.
	- Utilize Google Dorks, [Shodan.io](https://www.shodan.io/), [theHarvester](https://github.com/laramies/theHarvester), [Censys](https://censys.com/) or [Wayback Machine](https://archive.org/web/).
	- Gather any publicly available information about the target including leaks from breaches/incidents.
	- Look for DNS and WHOIS records.
- Study the web application's structure (utilize browser dev tools).
	- Frontend Components (HTML, CSS, JavaScript).
	- Look for endpoints in JavaScript files.
	- Core Functionality (Interaction between browser and server).
	- Assess the target from both authenticated and unauthenticated perspectives.
- Look for the following misconfigurations:
	- Missing SPF record
	- Missing DMARC record
	- Missing DKIM record
	- Missing security headers (Utilize [securityheaders.com](https://securityheaders.com/))
- Look for any public repositories owned by the target.
## Active Recon
- Identify if the application if using WAF
	- [wafw00f](https://github.com/EnableSecurity/wafw00f)
- Utilize general purpose automatic scanners.
	- Port scanning using Nmap.
	- Directory, DNS, and VHost fuzzing using [ffuf](https://github.com/ffuf/ffuf)or [GoBuster](https://github.com/OJ/gobuster).
	- Vulnerability scanning using [Nuclei](https://github.com/projectdiscovery/nuclei), [OpenVAS](https://github.com/greenbone/openvas-scanner), [Nikto](https://github.com/sullo/nikto), or Burp Active Scanner.
	- SSL/TLS scanning using [testssl.sh](https://github.com/drwetter/testssl.sh).
	- [reconFTW](https://github.com/six2dez/reconftw) or [recon-ng](https://github.com/lanmaster53/recon-ng)
- Enumerate for subdomains using [subfinder](https://github.com/projectdiscovery/subfinder) or [crt.sh](https://crt.sh/).
- Look for exposed Git folder, `.env` files, backup files, debug pages, and admin/staff-only pages during directory fuzzing.
- Check for default pages which might contain interesting information:
	- `robots.txt`
	- `sitemap.xml`
	- `crossdomain.xml`
	- `clientaccesspolicy.xml`
	- `/.well-known/`
- Enumerate and identify technologies used by the web application and server.
	- [WhatWeb](https://github.com/urbanadventurer/WhatWeb) or [Wappalyzer](https://www.wappalyzer.com/)
	- Look for known vulnerabilities in the version of the technology.
	- Utilize well-known tricks about the technology to extract more information.
- If target has CMS, identify CMS type and use the following:
	- WordPress: [wpscan](https://github.com/wpscanteam/wpscan)
	- Drupal/Silverstripe: [droopescan](https://github.com/SamJoan/droopescan)
## Source Code Review
If the source code of the application is open-source or has been made available to us.
- Study the contents of the CHANGELOG and README files.
- Look for information leakage and hardcoded credentials in the source code or commit history.
- Look for and understand currently open or recently closed issues submitted in the repository.
- Identify the encryption or hashing algorithm used.
## Common Features Checklist
### Authentication





# MERGE EVERYTHING BELOW ON CHECKLIST
### Input
- Test for Server-Side Includes Injection using various SSI directives.
### File Upload
- Fuzz the file upload functionality for whitelisted and blacklisted extensions
### Session Tokens
- Cookie Token Tampering
- Brute Force `rememberme` tokens
- Session Fixation Attack
- Session Hijacking
## Resources
- https://book.hacktricks.xyz/network-services-pentesting/pentesting-web
- https://book.hacktricks.xyz/pentesting-web/web-vulnerabilities-methodology
- https://pentestbook.six2dez.com/others/web-checklist
- https://github.com/Secuna/checklists/blob/main/web.md