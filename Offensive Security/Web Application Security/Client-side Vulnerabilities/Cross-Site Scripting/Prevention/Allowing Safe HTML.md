Some applications might allow users to content with limited HTML markup, however this must be avoided whenever possible.

The classic approach in protecting features like this from XSS is to create a whitelist of safe tags and attributes, and disallow JavaScript altogether. However, due to some discrepancies in browser parsing engines and quirks like mutation XSS, this approach is extremely difficult to implement.

The least bad option is to use a JavaScript library that performs filtering and encoding in the user's browser, such as DOMPurify. Other libraries allow users to provide content in markdown format and convert the markdown into HTML. Unfortunately, these libraries have XSS vulnerabilities from time to time, so you should monitor security updates closely.