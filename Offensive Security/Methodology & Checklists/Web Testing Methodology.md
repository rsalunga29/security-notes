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
	- Looked for leaked credentials using [developer tools and regex](https://github.com/h4x0r-dz/Leaked-Credentials/).
- Look for the following misconfigurations:
	- Missing SPF record.
	- Missing DMARC record.
	- Missing DKIM record.
	- Missing security headers ([securityheaders.com](https://securityheaders.com/)).
	- Look for cookies lacking security flags (https://www.invicti.com/learn/cookie-security-flags/).
- Look for any public repositories owned by the target.
## Active Recon
- Utilize general purpose automatic scanners.
	- Port scanning using Nmap.
	- Directory, DNS, and VHost fuzzing using [ffuf](https://github.com/ffuf/ffuf), [GoBuster](https://github.com/OJ/gobuster), or [amass](https://github.com/owasp-amass/amass).
	- Vulnerability scanning using [Nuclei](https://github.com/projectdiscovery/nuclei), [OpenVAS](https://github.com/greenbone/openvas-scanner), [Nikto](https://github.com/sullo/nikto), or Burp Active Scanner.
	- SSL/TLS scanning using [testssl.sh](https://github.com/drwetter/testssl.sh).
	- Spidering using [hakrawler](https://github.com/hakluke/hakrawler), [ParamSpider](https://github.com/devanshbatham/ParamSpider), or ZAP.
	- [reconFTW](https://github.com/six2dez/reconftw) or [recon-ng](https://github.com/lanmaster53/recon-ng) or [uncover](https://github.com/projectdiscovery/uncover).
- Enumerate for subdomains using [subfinder](https://github.com/projectdiscovery/subfinder) or [crt.sh](https://crt.sh/).
- Identify if the application if using WAF
	- [wafw00f](https://github.com/EnableSecurity/wafw00f)
	- Nmap's [http-waf-fingerprint](https://nmap.org/nsedoc/scripts/http-waf-fingerprint.html) script
- Look for exposed Git folder, `.env` files, backup files, debug pages, and admin/staff-only pages during directory fuzzing.
- Check for default pages which might contain interesting information:
	- `robots.txt`.
	- `sitemap.xml`
	- `crossdomain.xml`
	- `clientaccesspolicy.xml`
	- `/.well-known/`
- Enumerate and identify technologies used by the web application and server.
	- [WhatWeb](https://github.com/urbanadventurer/WhatWeb) or [Wappalyzer](https://www.wappalyzer.com/).
	- Look for known vulnerabilities in the version of the technology.
	- Utilize well-known tricks about the technology to extract more information.
- If target has CMS, identify CMS type and use the following:
	- WordPress: [wpscan](https://github.com/wpscanteam/wpscan).
	- Drupal/Silverstripe: [droopescan](https://github.com/SamJoan/droopescan).
## Source Code Review
If the source code of the application is open-source or has been made available to us.
- Study the contents of the CHANGELOG and README files.
- Look for information leakage and hardcoded credentials in the source code or commit history.
- Look for and understand currently open or recently closed issues submitted in the repository.
- Identify the encryption or hashing algorithm used.
- Identify and fuzz for sources and sinks for each functionality/feature.
## Common Features Checklist
### Authentication
#### Registration
- Check for common vulnerabilities and bypasses, including but not limited to:
	- Stored XSS or SSTI via reflected values such as name, email, etc.
	- SQL injection (manual and automated using sqlmap).
	- Server-Side Includes Injection using various SSI directives.
	- IDOR if interesting parameters exists (i.e `roleId`).
	- HTTP Verb Tampering.
	- HTTP Parameter Pollution.
- Existing user takeover via duplicate registration:
	- Changes in letter cases (uppercase, lowercase, camelcase).
	- Using unicode (i.e register as `ąďṁĩň` when `admin` already exists)
	- Add some dots in the emails.
	- Use special characters in the email (`%00`, `%09`, `%20`).
	- Manipulating email by adding additional `@` (i.e `victim@gmail.com@attacker.com`).
- Weak password policy:
	- Minimum of 8 characters with no maximum number.
	- Must allow numbers and special characters.
	- Must not allow dictionary word as password.
	- Long passwords (more than 200 chars) might lead to DoS.
- Social Media registration:
	- Check for OAuth.
	- Check for state parameter value.
- Corrupt registration and verification process:
	- 1. Sign up.
	- 2. Do not verify new account.
	- 3. Request for change/forgot password.
	- 4. Change password then check if account is active/verified.
- For JSON type requests, try manipulating JSON body by adding commas (i.e `{"email":"victim@gmail.com","hacker@mail.com","username":"defnothacker","password":"xxx"}`)
- Username uniqueness.
- Insufficient email verification process.
- Weak registration implementation or allows disposable email addresses.
- Fuzz after user creation to check if any folder have been overwritten or created with your profile name.
- Missing rate limit.
#### Login
- Check for common vulnerabilities and bypasses, including but not limited to:
	- SQL injection (manual and automated using sqlmap).
	- IDOR if interesting parameters exists (i.e `roleId`).
	- HTTP Verb Tampering.
	- HTTP Parameter Pollution.
- Check for response header and body, tamper with parameters to test for bypasses.
- Username/email enumeration via error message.
- Lack of defenses against brute force attacks.
- Test for default or common credentials.
- Test for resilience to password guessing:
	- Does the account get locked after number of failed attempts?
	- Does the application provide hints during failed attempts?
- If using OAuth or URL includes `/login?next=` of any sort, test for Open Redirection.
#### Forgot Password
- Check for common vulnerabilities and bypasses, including but not limited to:
	- Stored XSS or SSTI via reflected values such as name, email, etc.
	- Test for IDOR or HTTP Parameter Pollution if parameters includes identifiers such as IDs and username.
- Test for Password Reset Poisoning with HTTP Header Injection.
	- Add another `Host` or `X-Forwarded-Host` header.
- Username/email enumeration via error message.
- Test for reset token leak via URL or HTTP `Referer` header.
- Uniqueness of forget password reset links/codes.
	- Check which encryption/hashing algorithm is used for the tokens.
	- Look for any signs of sequential tokens in multiple requests.
- Validity and expiration time of reset links/codes.
	- Request 2 reset links and use the older one.
- If parameter includes email of account to reset password, check for carbon copy by using CRLF injection (i.e `email=victim@email.com%0a%0dcc:hacker@mail.com`).
#### Multi-factor Authentication
- Check for common vulnerabilities and bypasses, including but not limited to:
	- Guessable codes and race conditions.
	- Bypass via response manipulation.
	- Resilience to brute force.
#### JSON Web Tokens
- Check for common vulnerabilities and bypasses, including but not limited to:
	- Interesting values that can be changed (i.e `isAdmin`).
	- Secret keys resilience to dictionary-type brute force.
	- Change `alg` value to `none`.
- Parameter injections
	- RCE, SQLi, or LFI via key id (`kid`) parameter.
	- Injecting self-signed JWT via `jwk`, `jku`, or `kid` parameters.
- Timestamp tampering.
- [JWT Tool](https://github.com/ticarpi/jwt_tool).
### Updating Critical Information
- Check for common vulnerabilities and bypasses, including but not limited to:
	- Stored XSS or SSTI via reflected values such as name, email, etc.
	- SQL injection (manual and automated using sqlmap).
	- Server-Side Includes Injection using various SSI directives.
	- Test for IDOR or HTTP Parameter Pollution if parameters includes identifiers such as IDs and username.
- Check for pre-requisites before changing critical details:
	- Does it require a password or MFA before applying changes?
	- Does it require to input old password before applying new password?
### Session Management / Authorization
- Check for common vulnerabilities and bypasses, including but not limited to:
	- Cross Site Request Forgery.
	- SQL injection (manual and automated using sqlmap) via `Cookie` parameter.
	- LFI/RFI via `Cookie` parameter.
	- IDOR or HTTP Parameter Pollution for any parameters denoting session or authorization (roles).
	- Session Fixation Attack.
	- Session Hijacking.
- Test tokens for meaning and predictability.
- Test for improper implementation (i.e With privileged user perform privileged actions, try to repeat with unprivileged user cookie).
- If Cookie is Base64-encoded and decoded value looks like serialized object, test for Insecure Deserialization.
- Check `HTTPOnly` and `Secure` flags.
- Cookie Token Tampering.
- Cookie or "remember me" tokens resilience to brute force.
- Check cookie if it's still usable after logout.
- Cache issue, Logout then click back button.
- Insecure access control methods (request parameters, `Referer` header, etc.).
### Input / Parameter Validation
- XSS or SSTI via reflected values.
- HTTP Parameter Pollution.
- SQL injection (manual and automated using sqlmap).
- Server-Side Includes Injection using various SSI directives.
- If input / parameter accepts identifying strings (i.e ids), test for IDOR.
- If input / parameter is using XML, test for XXE Injection.
- If input / parameter is calling another URL, test for SSRF.
- If input / parameter accepts what looks like an OS command or value for an OS command, test for Command Injection.
- If input / parameter accepts a filename or directory, test for LFI/RFI.
- If input / parameter includes `/login?next=` of any sort, test for Open Redirection.
### File Uploads
- Fuzz the file upload functionality for file size limit and whitelisted/ blacklisted extensions and file types.
- Attempt to bypass filters and whitelists/blacklists to upload unwanted files.
	- If bypassed, chain with other vulnerabilities.
- Test for injections via filenames.
### Error Handling
- Force an error to see if the error message leaks unnecessary and sensitive information.
### Logging and Monitoring
- Does the application log authenticated/unauthenticated requests?
- Does the application log authorized/unauthorized requests?
- Does the application log sensitive data, such as passwords, tokens, PIIs, etc.?
- Check for verbosity of the logs.
### Application Logic
- Account deletion/disable option and try to reactivate with Forgot Password feature.
- Test multi-stage processes for logic flaws (i.e go from step 1 to step 4).
- Tamper or reuse gift or discount codes and alike.
- Test for HTTP Parameter Pollution and HTTP Verb Tampering.
### Web Proxies
- Cache Poisoning
- Cache Deception
- HTTP Request Smuggling
## Resources
- https://book.hacktricks.xyz/network-services-pentesting/pentesting-web
- https://book.hacktricks.xyz/pentesting-web/web-vulnerabilities-methodology
- https://pentestbook.six2dez.com/others/web-checklist
- https://github.com/Secuna/checklists/blob/main/web.md
- https://owasp.org/www-project-web-security-testing-guide/stable/
