Reflected XSS is the simplest variety of cross-site scripting. It arises when an application receives a malicious code in an HTTP request and executes that code within the immediate response in an unsafe way.

For example, suppose an application has a search function which receives the user-supplied search term in a URL parameter.
```txt
https://vulnerable-website.com/search?term=gift
```
The application echoes the supplied search term in the HTML:
```html
<p>You searched for: gift</p>
```
Assuming the application doesn't process the data, an attacker can construct an attack like this:
```txt
https://vulnerable-website.com/search?term=<script>alert(document.domain)</script>
```
If another user visits the attacker-supplied URL, the script will execute to open an alert popup containing the website's domain.