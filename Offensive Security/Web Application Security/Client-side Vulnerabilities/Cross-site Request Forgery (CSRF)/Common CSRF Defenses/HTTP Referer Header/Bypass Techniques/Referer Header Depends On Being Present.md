Some applications validate the `Referer` header when it is present in requests but skip the validation if the header is omitted.

In this situation, an attacker can create a CSRF payload in a way that causes the victim's browser to drop the `Referer` header in the resulting request. There are various ways to do this, but the easiest is using the following `<meta>` tag within the HTML page that hosts the payload:
```html
<meta name="referrer" content="never" />
```