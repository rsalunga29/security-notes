The pre-flight check was added to CORS to protect legacy resources from additional request options allowed by CORS. Essentially, it is a HTTP request using the `OPTIONS` method that is sent before the cross-origin request itself, in order to determine what methods and headers are permitted. And since this add an extra HTTP request round-trip, it increases the browsing overhead.

For example, the following is a pre-flight request that is seeking if `PUT` method and a custom request header called `Special-Request-Header` is allowed:
```http
OPTIONS /data HTTP/1.1
Host: normal-website.com
...
Origin: https://normal-website.com
Access-Control-Request-Method: PUT
Access-Control-Request-Headers: Special-Request-Header
```
The server might return a response like the following:
```http
HTTP/1.1 204 No Content
...
Access-Control-Allow-Origin: https://normal-website.com
Access-Control-Allow-Methods: PUT, POST, OPTIONS
Access-Control-Allow-Headers: Special-Request-Header
Access-Control-Allow-Credentials: true
Access-Control-Max-Age: 240
```
This response sets that the allowed methods are - `PUT`, `POST`, and `OPTIONS` and permitted request headers are `Special-Request-Header`. It also allows the sending of credentials, and the `Access-Control-Max-Age` header defines the maximum timeframe for caching the pre-flight request for reuse.