If a website uses public CDN platforms to load JavaScript, such as [unpkg.com](https://unpkg.com/), it is possible that the CSP tag or header is set to the following:
```html
<meta http-equiv="Content-Security-Policy" content="script src https://unpkg.com/">
```
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src https://unpkg.com/;
```

The problem with this approach is that it allows loading all libraries from this origin. Meanin