## Minifying JavaScript Code
A common way of reducing the readability of a snippet of JavaScript code while keeping it fully functional is JavaScript minification. Code minification means having the entire code in a single (often very long) line. This is done by using a [JavaScript minifier tool](https://www.toptal.com/developers/javascript-minifier).

For example, the following code:
```javascript
function hello() {
  console.log("Hello, World!")
}
```
Once minified, it will now look like this:
```javascript
function hello(){console.log("Hello, World!")}
```
## Packing JavaScript Code
Another way to obfuscate a JavaScript code is to use a technique called "packing", in which an [obfuscation tool](https://beautifytools.com/javascript-obfuscator.php) attempts to convert all words and symbols of the code into a list or dictionary and then refer to them using the `(p,a,c,k,e,d)` function to rebuild the original code during execution.

The `(p,a,c,k,e,d)` can be different from one packer to another, however, it usually contains a certain order in which the words and symbols were packed for it to know how to order them during the execution.

For example, the following code:
```javascript
function hello() {
  console.log("Hello, World!")
}
```
Once packed, it will turn into:
```javascript
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String)){while(c--){d[c]=k[c]||c}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('1 0(){2.3("4, 5!")}',6,6,'hello|function|console|log|Hello|World'.split('|'),0,{}))
```