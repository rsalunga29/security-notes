# TODO
Complete this methodology using following as guides: [HackTricks](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web) and [Pentest Book](https://pentestbook.six2dez.com/others/web-checklist).
Create a checklist for each steps.
Create a checklist for each vulnerability types (optional).
## Draft
1. Review the web app's frontend component (HTML, CSS, JavaScript) using "View Page Source" in Dev Tools, and look for Sensitive Data Exposure or Cross-Site Scripting vulnerabilities.
2. After thoroughly testing all frontend components, review the web app's core functionality to review the interaction between browser and server.
3. Enumerate the web technologies used by the web server and look for exploitable flaws.
4. Assess web app from both authenticated and unauthenticated perspectives.
### File Upload
- Fuzz the file upload functionality for whitelisted and blacklisted extensions
### Input
- Test for Server-Side Includes Injection using various SSI directives.
## Preparation
- Understand the business area and what the customer needs.
- Study the web application's structure.
	- Frontend Components (HTML, CSS, JavaScript)
	- Core Functionality (Interaction between browser and server)
## Recon