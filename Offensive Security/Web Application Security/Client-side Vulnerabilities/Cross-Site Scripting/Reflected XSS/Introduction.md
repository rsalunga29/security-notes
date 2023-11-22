Reflected XSS is the simplest variety of cross-site scripting. It arises when an application receives a malicious code in an HTTP request and executes that code within the immediate response in an unsafe way.

For example, suppose an application has a search function which receives the user-supplied search term in a URL parameter.
```txt
https://vulnerable-website.com/search?term=gift
```
The application echoes the supplied search term in the HTML:
```html
<p>You searched for: gift</p>
```
