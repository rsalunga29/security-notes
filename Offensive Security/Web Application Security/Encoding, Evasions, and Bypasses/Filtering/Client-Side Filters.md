Another approach to filter/block attacks is using client-side filters within web browsers. These browsers are the primary means used to address attacks. The goal of client-side defenses is to protect users against vulnerabilities in web applications.
## Browser Add-ons
The [NoScript Security Suite](https://addons.mozilla.org/en-US/firefox/addon/noscript/) is an extension for Firefox and is the first valid solution for client-side filtering.

NoScript is a whitelist-based security tool that basically disables all the executable web content, such as, JavaScript, Java Flash, Silverlight, etc. It also lets the user to choose which sites are trusted.
## Native Browser Filters
The first attempt at blocking malicious requests natively was made by Microsoft and introduced in IE8, called **XSS Filter**. Afterwards, Google Chrome did the same and introduced **XSS Auditor**.
### XSS Filter (IE)
The XSS Filter rules are hardcoded in the `c:\windows\system32\mshtml.dll` library. Inspecting them is as easy as:
```cmd
findstr /C:"sc{r}" \WINDOWS\SYSTEM32\mshtml.dll | find "{"
```
While the XSS Filter has few rules - 25 to be exact, they are well constructed and difficult to attack. Even with bypasses being discovered over the years, the latest versions seems to be stronger than the past versions.

The XSS Filter works by "neutering" characters. Basically, once a malicious injection is detected, the XSS Filter modifies the evil part of the payload by adding the `#` character, defined in the rules. For example:
- `<svg/onload=alert(1)>` is transformed to `<svg/#nload=alert(1)>`.
- `<isindex/onmouseover=alert(1)>` is transformed to `<is#ndex/#nmouseover=alert(1)>`.
#### X-XSS-Protection Header
Websites who chose to disable XSS Filter, can use the `X-XSS-Protection` HTTP header instead. It can be used as such:
```http
HTTP/1.1 200 OK
...
X-XSS-Protection: 1; mode=block
```
### XSS Auditor (WebKit/Blink)
This is enabled by default in browsers such as Google Chrome, Opera and Safari. Authors of XSSAuditor claims the filter design is both effective and highly precise. To do this, they placed XSS Auditor in between the HTML Parser and JS engine.

The filter analyzes both the inbound requests and the outbound. If, in the parsed HTML data, it finds executable code within the response, then it stops the script and generates a console alert.

However, there are tons of bypasses for XSS Auditor. In fact, a simple search on google about XSS Auditor returns more information on bypasses than on the filter itself.