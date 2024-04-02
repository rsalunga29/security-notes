If a website uses public CDN platforms to load JavaScript, such as [unpkg.com](https://unpkg.com/), it is possible that the CSP tag or header is set to the following:
```html
<meta http-equiv="Content-Security-Policy" content="script src https://unpkg.com/">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src https://unpkg.com/;
```

The problem with this approach is that it allows loading all libraries from this origin. Meaning, if a malicious library is uploaded in [unpkg.com](https://unpkg.com/), an attacker can use it and bypass CSP to perform XSS attacks.

For testing this, someone has already created a library called [csp-bypass](https://github.com/CanardMandarin/csp-bypass) and uploaded it. The payload to use will be:
```txt
http://target-website.com/?name=<br csp="alert(1)">
```