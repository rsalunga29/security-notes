Some XSS context can be found inside JavaScript within the response. In this situation, a wide variety of results can arise, with different techniques necessary to successfully perform an exploit.
## Terminating Existing Script
In the simplest case, it is possible to simply close the script tag in the existing JavaScript, and introduce a new HTML tag that will trigger the execution of JavaScript. For example, if the XSS context is as follows:
```js
<script>
var input = 'controllable data here';
</script>
```
An attacker can simply use the following payload to break out of existing JavaScript and execute their payload:
```html
';</script><img src=1 onerror=alert(document.domain) />
```
## Breaking Out of a JavaScript String
Some XSS contexts are inside a quoted string literal. The following are some useful ways of breaking out of a string literal:
```js
'-alert(document.domain)-'
```
```js
';alert(document.domain)//
```
It is important to repair or comment out the script following the XSS payload, as any syntax error will prevent the whole script from executing.

However, some applications escapes single or double-quote characters with a backslash, which tells the JavaScript parser to interpret it as a string instead of as a special character. You can attempt to bypass this by neutralizing the backslash added by the application using your own backslash character. For example, suppose the input:
```js
';alert(documen)
```