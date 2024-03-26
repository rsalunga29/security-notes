Websites may also store data on the server and reflect it elsewhere. In a stored DOM XSS vulnerability, the server receives data from one request, stores it, and then includes the data in a later response. A script within the later response contains a sink which then processes the data in an unsafe way. For example:
```js
element.innerHTML = comment.author
```