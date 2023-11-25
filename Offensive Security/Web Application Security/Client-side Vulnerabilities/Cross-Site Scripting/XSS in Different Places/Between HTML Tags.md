When the XSS context is text between HTML tags, you need to introduce some new HTML tags designed to trigger execution of JavaScript.

Some useful ways of executing JavaScript are:
```html
<script>alert(document.domain)</script>
<img src=1 onerror=alert(document.domain)>
```
## XSS w/ Most Tags and Attributes Blocked
1. In Burp Intruder, in the Positions tab, replace the value of the search term with: `<>`
2. Place the cursor between the angle brackets and click "Add §" twice, to create a payload position. The value of the search term should now look like: `<§§>`
3. Visit the [XSS cheat sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet) and click "Copy tags to clipboard".
4. In Burp Intruder, in the Payloads tab, click "Paste" to paste the list of tags into the payloads list. Click "Start attack". 
5. Once the allowed tag is found, go back to positions and place the cursor before the `=` character (i.e `<body §§=1>`).
## XSS w/ All Tags Blocked Except For Custom Tags
