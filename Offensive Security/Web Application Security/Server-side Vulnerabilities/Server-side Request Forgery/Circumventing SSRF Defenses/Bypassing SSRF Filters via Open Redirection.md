It is sometimes possible to bypass filter-based defenses by exploiting an open redirection vulnerability.

For example, imagine a user-submitted URL is strictly validated to prevent exploitation of the SSRF behavior. However, the whitelisted URLs contains an open redirection vulnerability. For Example:

Provided that the backend API supports redirections, you can manipulate the URL that satisfies the filter and results in a redirected request to the target URL.
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=/product/nextProduct?currentProductId=6&path=http://192.168.0.68/admin
```
In this example, we noticed that another part of the application receives a URL to redirect to next product


This will return a redirection to `http://192.168.0.68/admin` exposing the administrative interface. This exploit works because the application can validate that the `stockApi` parameter value is a on a whitelisted domain list, wherein the application requests the supplied URL and triggers the open redirection by following the redirection and making a request.