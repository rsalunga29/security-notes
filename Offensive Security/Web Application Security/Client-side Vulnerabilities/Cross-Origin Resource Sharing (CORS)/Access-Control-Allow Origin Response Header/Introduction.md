The `Access-Control-Allow-Origin` (ACAO) header is included in the response from one website to a request originating from another website, and identifies the permitted origin of the request. A web browser compares the `Access-Control-Allow-Origin` with the requesting website's origin and permits access to the response if they match.

The CORS specification identifies a collection of protocol of which `Access-Control-Allow-Origin` is the most significant. This header is returned by the server when a website requests a cross-domain resource, with an `Origin` header added by the browser.

For example, suppose `normal-website.com` causes a cross-domain request to `robust-website.com`:
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
The browser will allow code running on `normal-website.com` to access the response because the origins match.

The `Access-Control-Allow-Origin` also allows for multiple origins or the usage of `null` or the wildcard `*`. However, no browser supports multiple origins and there are restrictions on the use of the wildcard `*`.