 When the XSS context is into an HTML tag attribute value, you might sometimes be able to terminate the attribute value, close the tag, and introduce a new one. For example:
 ```html
 "><script>alert(document.domain)</script>
```
However, most situations like this, angle brackets are either blocked or encoded making it harder for the input to break out of the tag in which it appears. Alternatively, you can introduce a new attribute that creates a scriptable context, provided you can terminate the attribute value. For example:
```html
" autofocus onfocus=alert(document.domain) x="
```
The above payload will result in an `input` tag like the following:
```html
<input type="text" name="search" value="" autofocus onfocus="alert(document.domain)" x="">
```
It basically created an `onfocus` event that will execute JavaScript when the element receives the focus, and also adds the `autofocus` attribute to try to trigger the `onfocus` event automatically without any user interaction. Finally, it adds `x="` to repair the following markup.
## Scriptable HTML Tag Attribute
Some HTML tag attributes allows JavaScript to be executed without needing to terminate the attribute value. In the context of the anchor tag, the `href` attribute can be used with the `javascript:` pseudo-protocol to execute a script. For example:
```html
<a href="javascript:alert(document.domain)" />
```