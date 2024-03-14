# TODO
Complete this methodology using following as guides: [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web) and [Pentest Book](https://pentestbook.six2dez.com/others/web-checklist).
Create a checklist for each steps.
Create a checklist for each vulnerability types (optional).
## Recon
- Understand the business area and what the customer needs.
- Perform OSINT on the target.
	- Gather any publicly available information about the target.
	- Look for employees or contractors associated with the target.
- Study the web application's structure (utilize browser dev tools).
	- Frontend Components (HTML, CSS, JavaScript)
	- Core Functionality (Interaction between browser and server)
	- Assess the target from both authenticated and unauthenticated perspectives.
- Enumerate and identify technologies used by the web application and server.
	- Look for known vulnerabilities in the version of the technology.
	- Utilize well-known tricks about the technology to extract more information.
	- [WhatWeb](https://github.com/urbanadventurer/WhatWeb)
	- [Wappalyzer](https://www.wappalyzer.com/)
## Automated Recon
- Launch general purpose scanners
## Source Code Review
If the source code of the target application is open-source or has been made available to us.
- Study the contents of the changelog and README.
- Look for any hardcoded credentials.
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