Also known as XSS, is a web security vulnerability that allows an attacker to execute malicious scripts in a victim's browser by injecting malicious code in a legitimate website. When the malicious code executes, the attacker can fully compromise their interaction with the application. For example:
```txt
https://vulnerable-website.com?query=<script>alert(document.domain)</script>
```
The URL above will show a JavaScript alert containing the target website's domain. Fortunately, since Chrome version 92, cross-origin iframes are prevented from calling `alert()`, however an attacker can still use the `print()` function as an [alternative](https://portswigger.net/research/alert-is-dead-long-live-print).

In worst cases, an attacker can also use Cross-Site Scripting to steal other user's cookies and impersonate as a legitimate user.
## Cheat Sheet
This [cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) contains some example of useful syntax that you can use to perform a XSS, it also contains helpful syntax to bypass WAFs and filters.