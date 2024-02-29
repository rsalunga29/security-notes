Most XSS can be prevented by encoding data on output, validating input upon arrival, and creating a whitelist of allowed values.
## Encode Data on Output
Output data must be encoded before it is written to a page, this is to prevent browsers from interpreting user-supplied or untrusted data as part of the web page code. The encoding you should use will be determined by the context you're writing into. For example, values inside a JavaScript string require a different type of escaping to those in an HTML context.

For example, in an HTML context, converting non-whitelisted values into HTML entities will look like these:
- `<` converts to `&lt;`
- `>` converts to `&gt;`

While in a JavaScript context, non-alphanumeric values should be Unicode-escaped:
- `<` converts to `\u003c`
- `>` converts to `\u003e`

There will also be times where multiple layers of encoding must be applied, in the correct order. For example, to safely embed a user-supplied input inside an event handler, you need to first Unicode-escape the input and then HTML-encode it.
## Validate Input on Arrival
Encoding user-supplied data is not sufficient to prevent XSS in every context. It is also important to strictly validate the input at the point when it is first received from a user.

Example of input validation include:
- If a user submits a URL, validating that it starts with a safe protocol such as HTTP and HTTPS will prevent someone from exploiting your application with a harmful protocol like `javascript` or `data`.
- If the input expects a value to be numeric, make sure to validate that the value actually contains an integer.
- Validating that input contains only an expected set of characters.
- Do not allow any input with JavaScript code in it, the library [DOMPurify](https://github.com/cure53/DOMPurify) can assist in implementing this.

Ideally, input validating should block invalid inputs. An alternative approach would be to attempt to clean invalid input to make it valid, but this is more prone to errors and must be avoided when necessary.
## Whitelisting vs Blacklisting
Employing whitelists is much better rather than blacklists, as this will future proof your application defenses when new harmful contents appear and make it less susceptible to attacks that seek to evade your blacklist by obfuscating invalid values.

For example, instead of trying to make a list of harmful protocols, such as `javascript`, `data`, etc., it is easier to simply make a list of safe protocols, such as HTTP and HTTPS.