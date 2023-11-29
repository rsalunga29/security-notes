Most XSS can be prevented by encoding data on output and validating input upon arrival.
## Encode Data on Output
Output data must be encoded before it is written to a page, this is to prevent browsers from interpreting user-supplied or untrusted data as part of the web page code. The encoding you should use will be determined by the context you're writing into. For example, values inside a JavaScript string require a different type of escaping to those in an HTML context.

For example, in an HTML context, converting non-whitelisted values into HTML entities will look like these:
- `<` converts to `&lt;`
- `>` converts to `&gt;`

While in a JavaScript context, non-alphanumeric values should be Unicode-escaped:
- `<` converts to `\u003c`
- `>` converts to `\u003e`

There will also be times where multiple layers of encoding must be applied, in the correct order.
## Validate Input on Arrival
Lorem ipsum..