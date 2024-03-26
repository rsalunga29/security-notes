Some applications validate the `Referer` header in a way that it can be bypassed. For example, if the application verifies that the `Referer` header starts with `vulnerable-website.com`, then the attacker can place this as a subdomain of their own domain:
```txt
https://vulnerable-website.com.attacker-website.com/csrf-attack
```

Likewise, if the application only validates whether the `Referer` header contains its own domain name, the attacker can place the require value elsewhere in the URL, for example:
```txt
https://attacker-website.com/csrf-attack?vulnerable-website.com
```
This method won't always work as many browsers now strip the query string (`?`) from the `Referer` header by default. However, an attacker can override this behavior by making sure that the website containing their exploit has the `Referrer-Policy: unsafe-url` header set.