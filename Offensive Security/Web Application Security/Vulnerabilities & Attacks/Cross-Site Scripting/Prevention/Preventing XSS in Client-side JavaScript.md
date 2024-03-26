In order to escape user-supplied input in an HTML context in JavaScript, you need to create your own functions to HTML-encode or Unicode-escape the inputs, as JavaScript doesn't provide an API to do both.

The following is an example JavaScript code to convert strings into HTML entities:
```js
function htmlEncode(str){
    return String(str).replace(/[^\w. ]/gi, function(c){
        return '&#'+c.charCodeAt(0)+';';
    });
}
```
The function will be used as follows:
```html
<script>
document.body.innerHTML = htmlEncode(untrustedValue)
</script>
```

The following example is an example JavaScript code that performs Unicode-escaping:
```js
function jsEscape(str){
    return String(str).replace(/[^\w. ]/gi, function(c){
        return '\\u'+('0000'+c.charCodeAt(0).toString(16)).slice(-4);
    });
}
```
The function will be used as follows:
```html
<script>
document.write('<script>x="'+jsEscape(untrustedValue)+'";
</script>
```