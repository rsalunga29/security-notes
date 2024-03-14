# TODO
Complete this methodology using following as guides: [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web) and [Pentest Book](https://pentestbook.six2dez.com/others/web-checklist).
Create a checklist for each steps.
Create a checklist for each vulnerability types (optional).
## Passive Recon
- Understand the business area and what the customer needs.
- Perform OSINT on the target.
	- Utilize Google Dorks, [Shodan.io](https://www.shodan.io/), [Censys](https://censys.com/).
	- Gather any publicly available information about the target.
	- Look for contact information of employees or contractors associated with the target.
- Study the web application's structure (utilize browser dev tools).
	- Frontend Components (HTML, CSS, JavaScript).
	- Look for endpoints in JavaScript files.
	- Core Functionality (Interaction between browser and server).
	- Assess the target from both authenticated and unauthenticated perspectives.
- Look for the following misconfigurations:
	- Missing SPF record
	- Missing DMARC record
	- Missing DKIM record
	- Missing security headers
- Look for any public repositories owned by the target.
## Active Recon
- Identify if the application if using WAF
	- [wafw00f](https://github.com/EnableSecurity/wafw00f)
- Utilize general purpose automatic scanners.
	- Port scanning using Nmap.
	- Directory, DNS, VHost fuzzing using ffuf or GoBuster.
	- Vulnerability scanning using Nuclei, OpenVAS, or Burp Active Scanner.
- Enumerate and identify technologies used by the web application and server.
	- [WhatWeb](https://github.com/urbanadventurer/WhatWeb)
	- [Wappalyzer](https://www.wappalyzer.com/)
	- Look for known vulnerabilities in the version of the technology.
	- Utilize well-known tricks about the technology to extract more information.
## Source Code Review
If the source code of the application is open-source or has been made available to us.
- Study the contents of the CHANGELOG and README files.
- Look for information leakage and hardcoded credentials in the source code or commit history.
- Look for and understand currently open or recently closed issues submitted in the repository.
- Identify the encryption or hashing algorithm used.
## Checklist
### Input
- Test for Server-Side Includes Injection using various SSI directives.
### File Upload
- Fuzz the file upload functionality for whitelisted and blacklisted extensions
### Session Tokens
- Cookie Token Tampering
- Brute Force `rememberme` tokens
- Session Fixation Attack
- Session Hijacking