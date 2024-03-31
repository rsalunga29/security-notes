Content Security Policy, also known a  CSP, is a web security mechanism that aims to mitigate XSS and some other attacks. The CSP works by restricting the resources that a page can load and whether a page can be framed by other pages. For example, the CSP can be used to restrict loading external scripts or allowing inline scripts to be executed.

To enable CSP, a response needs to include the header `Content-Security-Policy` containing the policy value which itself consists of one or more directives, separated by semicolons. For example:
```http
HTTP/1.1 200 OK
...
Content-Security-Policy: script-src js.cdn-website.com; img-src 'self';
```
The directive `script-src` will only allow JavaScript to be loaded from the specified domain `js.cdn-website.com`. While the `img-src` will only allow images to be loaded from the same origin as the page itself.

Alternatively, you can also apply CSP via the `<meta>` tag. For example:
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">
```