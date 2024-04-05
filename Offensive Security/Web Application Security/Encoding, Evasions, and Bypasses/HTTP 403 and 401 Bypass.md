## HTTP Verbs/Methods Fuzzing
Try using different verbs/methods to access the page then enumerate the value of response headers, maybe some additional information may be given. For example, a `200 OK` response to `HEAD` verb with `Content-Length: 55` means that the `HEAD` verb can access the info.

We can also use the `X-HTTP-Method-Override` header to overwrite the verb that is being used.

Additionally, when using `TRACE` verb, there are chances where we can also see the headers added by intermediate proxies in the response.
## HTTP Headers Fuzzing
<!-- TODO: Link HTTP Request Smuggling -->
- Change `Host` header to some arbitrary value. For example, if we changed it from `Host: target-website.com` to `Host: google.com`, the access control mechanism might fail and allow access to protected resource.
- Try to use other `User-Agents` or completely remove the `Host` header to access the resource.
- Fuzz HTTP headers by using HTTP Proxy Headers, below is a list of possible headers to use:
	- `X-Originating-IP: 127.0.0.1`
	- `X-Forwarded-For: 127.0.0.1`
	- `X-Forwarded: 127.0.0.1`
	- `Forwarded-For: 127.0.0.1`
	- `X-Remote-IP: 127.0.0.1`
	- `X-Remote-Addr: 127.0.0.1`
	- `X-ProxyUser-Ip: 127.0.0.1`
	- `X-Original-URL: 127.0.0.1`
	- `Client-IP: 127.0.0.1`
	- `True-Client-IP: 127.0.0.1`
	- `Cluster-Client-IP: 127.0.0.1`
	- `X-ProxyUser-Ip: 127.0.0.1`
	- `Host: localhost`
- If the path is protected, use the following headers to attempt to bypass the path protection:
	- `X-Original-URL: /admin/console`
	- `X-Rewrite-URL: /admin/console`
- If the page is behind a proxy, try HTTP Request Smuggling or Hop-by-Hop Headers.
## Protocol Version
If using `HTTP/1.1` try to use `1.0` or even test if it supports `2.0`.
## Path Fuzzing
If the path is protected, try to use encoding or multiple encodings to attempt to bypass the access control mechanism.

Additionally, the access control mechanism might not be case-sensitive, so try changing the case for each character. Example below:
- `target-website.com/admin` returns `403 Forbidden`.
- `target-website.com/ADMIN` returns `200 OK`.
- `target-website.com/admin/` returns `200 OK`.
- `target-website.com//admin//` returns `200 OK`.
- `target-website.com/;/admin` returns `200 OK`.
- etc...

<!-- TODO: Link Parameter Pollution -->
Finally, if the target is an API, try changing the API versions, the data type of the request body, or perform Parameter Pollution. For example:
- `/v3/users_data/id=1234` returns `403 Forbidden`.
- `/v1/users_data/id=1234` returns `200 OK`.
- `{"id": 1234}` returns `401 Unauthorized`.
- `{"id": [1234]}` returns `200 OK`.
- `{"id":{"id":111}}` returns `200 OK`.
- `{"user_id":"<legit_id>","user_id":"<victims_id>"}` (JSON Parameter Pollution)