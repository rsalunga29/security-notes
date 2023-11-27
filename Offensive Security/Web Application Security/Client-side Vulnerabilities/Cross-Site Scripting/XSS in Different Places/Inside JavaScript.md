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
##