The [Content Security Policy](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FContent%20Security%20Policy%2FIntroduction) (CSP) is the last line of defense against cross-site scripting vulnerabilities. If any other XSS prevention fails, the CSP can be used to restrict what an attacker could do.

An example CSP is as follows:
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: default-src 'self'; script-src 'self'; object-src 'none'; frame-src 'none'; base-uri 'none';
```
This policy specifies that resources such as images and scripts can only be loaded from the same origin as the main page, which greatly reduces an attacker's attack surface.

If loading of external resources can't be avoided, ensure to only allow scripts that can't be used by an attacker to aid their exploit. For example, if a certain domain is whitelisted then an attacker can load any script from those domains. Whenever possibly, try to host resources on your own domain.

Alternatively, using the 