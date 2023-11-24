Testing for DOM-based vulnerabilities manually needs a browser with developer tools, such as Chrome. You need to work through each available source and test each one individually.
## Testing HTML Sinks
Testing for DOM XSS in HTML sink can be started by placing a random alphanumeric string into a source, such as `locatiton.search`, then use developer tools to inspect the HTML and find where the string appears.

After finding the injected string, identify the context. Based on this context, the input must be refined to determine how it is processed. For example, if the string appears in a double-quoted attribute, try injecting double quotes in the string and see if you can break out of the attribute.

Some browsers URL-encode values from `location.search` and `location.hash`. If the injected string gets URL-encoded before being processed, then an XSS attack is unlikely to work.
## Testing JavaScript Execution Sinks
Testing for JavaScript execution sinks is a little harder. The JavaScript debugger will be used to determine whether and how the input it sent to a sink.

For each potential source, such as `location`, it is important to find cases within the page's JavaScript code where the source is being referenced/read.

1. Once found, use the JS debugger to add a break point and follow how the source's value is being used.
2. If the source gets assigned to other variables, you need to track these variables and see if they're passed to a sink.
3. Once the sink that is receiving the data from the source is found, use the debugger to inspect the value by hovering over the variable to show its value before it is sent to the sink
4. Refine the input to deliver a successful XSS attack
## Testing using DOM Invader
Identifying and exploiting DOM XSS in the wild can be a tedious process, often requiring you to manually trawl through complex, minified JavaScript. If you use Burp's browser, however, you can take advantage of its built-in [DOM Invader extension](https://portswigger.net/burp/documentation/desktop/tools/dom-invader), which does a lot of the hard work for you.