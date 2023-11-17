The `Access-Control-Allow-Origin` response header indicates whether the response can be shared with the requested code from the given origin. For example, suppose `normal-website.com` causes a cross-domain request to `robust-website.com`:
```http
GET /data HTTP/1.1
Host: robust-website.com
Origin: normal-website.com
```
The server running `robust-website.com` will then return the following response:
```http
HTTP/1.1 200 OK
...
Access-Control-Allow-Origin: normal-website.com
```
The browser will then compare if `Access-Control-Allow-Origin` value is the same as the requesting website's origin, in this case `normal-website.com`, and permits the response if they match.

The `Access-Control-Allow-Origin` also allows for multiple origins or the usage of `null` or the wildcard `*`. However, no browser supports multiple origins and there are restrictions on the use of the wildcard `*`:
- When `Access-Control-Allow-Origin` is set to the wildcard `*`, it disallows the use cross-origin transfer of credentials.
- Wildcards cannot be used within any other value. For example, the following header is not valid:
```txt
Access-Control-Allow-Origin: *.normal-website.com
```