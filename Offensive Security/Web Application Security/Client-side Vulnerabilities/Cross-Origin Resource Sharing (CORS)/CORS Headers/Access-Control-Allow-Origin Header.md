The `Access-Control-Allow-Origin` response header indicates whether the response can be shared with the requested code from the given origin. For example, suppose `normal-website.com` causes a cross-domain request to `robust-website.com`:
```http
GET /data HTTP/1.1
Host: robust-website.com
Origin : https://normal-website.com
```
The server running `robust-website.com` will then return the following response:
```http
HTTP/1.1 200 OK
...
Access-Control-Allow-Origin: https://normal-website.com
```
The browser will then compare if `Access-Control-Allow-Origin` value with the requesting website's origin, this example `normal-website.com`, and permits the response if they match.

The `Access-Control-Allow-Origin` also allows for multiple origins or the usage of `null` or the wildcard `*`. However, no browser supports multiple origins and there are restrictions on the use of the wildcard `*`.



The CORS specification identifies a collection of protocol of which `Access-Control-Allow-Origin` is the most significant. This header is returned by the server when a website requests a cross-domain resource, with an `Origin` header added by the browser.