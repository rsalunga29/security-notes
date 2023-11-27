Also known as CSP, is a web security mechanism that aims to mitigate XSS and some other attacks. The CSP works by restricting the resources that a page can load and whether a page can be framed by other pages.

To enable CSP, a response needs to include the header `Content-Security-Policy` containing the policy value which itself consists of one or more directives, separated by semicolons. For example:
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src 'self' js.website.com; object-src 'self';
```

Alternatively, you can also apply CSP via the `<meta>` tag. For example:
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">
```