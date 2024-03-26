The most common form of XSS in jQuery is when you pass user input to a jQuery selector. Web developers would often use `location.hash` and pass it to the selector which would cause XSS as jQuery would render the HTML. jQuery recognized this issue and patched their selector logic to check if input begins with a hash. Now jQuery will only render HTML if the first character is a `<`. If you pass untrusted data to the jQuery selector, ensure you correctly escape the value using the following function:
```js
function jsEscape(str){
    return String(str).replace(/[^\w. ]/gi, function(c){
        return '\\u'+('0000'+c.charCodeAt(0).toString(16)).slice(-4);
    });
}
```