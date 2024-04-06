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

If we already know or able to guess the sequence, then we could create more complex payloads for bypass