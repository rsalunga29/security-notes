File inclusion vulnerabilities allow an attacker to read sensitive files or sometimes execute files on a server. The vulnerability occurs due to the use of user-supplied input without proper validation.

There are two types of file inclusions:
1. Local File Inclusion (LFI) - Returns a local server file, in worst cases an LFI can chained into a remote code execution
2. Remote File Inclusion (RFI) - The file is loaded from a remote server. Since PHP5, this is disabled by default with the config `allow_url_include`.

This vulnerability is usually chained with [Path Traversal](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FPath%20Traversal%2FIntroduction) and [Server Side Request Forgery (SSRF)](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FServer-side%20Request%20Forgery%2FIntroduction), as this vulnerability requires one or the other to properly work.
## PHP
In PHP, we may use the `include()` function to load a local or a remote file as we load a page. If the path passed to the `include()` is taken from a user-controlled parameter, like a GET parameter, and the code does not explicitly filter and sanitize the user input, then the code becomes vulnerable to File Inclusion. For example:
```php
if (isset($_GET['language'])) {
    include($_GET['language']);
}
```
This vulnerability is not exclusive to the `include()` function, as there are many other PHP functions that would lead to the same vulnerability if we had control over the path passed into them. Such functions include `include_once()`, `require()`, `require_once()`, `file_get_contents()`, and several others as well.
## NodeJS
Just as the case with PHP, NodeJS web servers may also load content based on an HTTP parameters. The following is a basic example of how a GET parameter `language` is used to control what data is written to a page:
```js
if(req.query.language) {
    fs.readFile(path.join(__dirname, req.query.language), function (err, data) {
        res.write(data);
    });
}
```
Another example is the `render()` function in the Express.js framework. The following example shows uses the `language` parameter to determine which directory it should pull the `about.html` page from:
```js
app.get("/about/:language", function(req, res) {
    res.render(`/${req.params.language}/about.html`);
});
```
Unlike our earlier examples where GET parameters were specified after a (`?`) character in the URL, the above example takes the parameter from the URL path (e.g. `/about/en` or `/about/es`).
## Java
The following examples show how web applications for a Java web server may include local files based on the specified parameter, using the `include` function:
```jsp
<c:if test="${not empty param.language}">
    <jsp:include file="<%= request.getParameter('language') %>" />
</c:if>
```
The `import` function may also be used to render a local file or a URL, such as the following example:
```jsp
<c:import url= "<%= request.getParameter('language') %>"/>
```
## .NET
The `Response.WriteFile` .NET function works very similarly to our examples above. It takes a file path for its input and writes its content to the response. For example:
```cs
@if (!string.IsNullOrEmpty(HttpContext.Request.Query['language'])) {
    <% Response.WriteFile("<% HttpContext.Request.Query['language'] %>"); %> 
}
```
Furthermore, the `@Html.Partial()` function may also be used to render the specified file as part of the front-end template
```cs
@Html.Partial(HttpContext.Request.Query['language'])
```
Finally, the `include` function may be used to render local files or remote URLs, and may also execute the specified file as well.
```cs
<!--#include file="<% HttpContext.Request.Query['language'] %>"-->
```