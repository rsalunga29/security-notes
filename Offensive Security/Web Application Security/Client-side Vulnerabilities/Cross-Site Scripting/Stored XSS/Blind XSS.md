Blind XSS vulnerabilities are a variant of stored XSS vulnerabilities. They occur when an attacker input is saved in the database and executed as a malicious script in another part of the application or in another application. For example, an attacker injects a malicious payload into a contact/feedback page and when the administrator of the application is reviewing the feedback entries the attacker’s payload will be loaded.

Other example of web applications or pages where blind XSS may occur:
- Log viewers
- Exception handlers
- Chat applications / forums
- Customer ticket applications
- Product reviews
- Any application that requires user moderation by certain users (e.g Admins)