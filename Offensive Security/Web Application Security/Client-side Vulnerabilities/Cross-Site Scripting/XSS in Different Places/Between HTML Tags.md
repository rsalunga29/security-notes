When the XSS context is text between HTML tags, you need to introduce some new HTML tags designed to trigger execution of JavaScript.

Some useful ways of executing JavaScript are:
```html
<script>alert(document.domain)</script>
<img src=1 onerror=alert(document.domain)>
```