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

The XSS Filter works by "neutering" characters. Basically, once a malicious injection is detected, the XSS Filter modifies the evil part of the payload by adding the `#` character, defined in the rules. For example:
- `<svg/onload=alert(1)>` is transformed to `<svg/#nload=alert(1)>` using the filter `{[ /+\t\"\'`]{o}n\c\c\c+?[ +\\t]*?=.}`
- 