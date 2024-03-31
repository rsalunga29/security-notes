Also known as Folder Path Bypass. If the CSP policy points to a directory that is safe to load scripts from. For example:
```html
<meta http-equiv="Content-Security-Policy" content="script src 'nonce-abcd1234'">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src 'nonce-abcd1234';
```