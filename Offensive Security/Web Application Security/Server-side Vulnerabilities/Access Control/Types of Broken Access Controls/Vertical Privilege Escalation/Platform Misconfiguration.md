Some applications enforce access controls at the platform layer. They do this by restricting access to specific URLs and HTTP methods based on the user's role. For example, an application might configure a rule as follows:
```txt
DENY: POST, /admin/deleteUser, managers
```
This rule denies access to HTTP `POST` method on the URL `/admin/deleteUser`, for users in the managers group. Various things can go wrong in this situation, leading to access control bypass.

Some application frameworks support various non-standard HTTP headers that can be used to override the URL in the original request, such as `X-Original-URL` and `X-Rewrite-URL`. If a website uses rigorous front-end controls to restrict access based on the URL, but the application allows the URL to overridden via a request header, then it might be possible to bypass the access control using the request like the following:
```
POST / HTTP/1.1
X-Original-URL: /admin/deleteUser
```

In order to test if frameworks support `X-Original-URL` and `X-Rewrite-URL`, we can do the following:
1. Send request to Burp Repeater
2. Change the URL in the request line to `/` and add the HTTP Header `X-Original-URL: /invalid-route`. If the application returns a 404 Response, it might indicate that the backend system is processing the URL from the `X-Original-Header`
	1. If the target URL requires a parameter, change the URL in request line to `/?parameter=value`
3. Change the value of `X-Original-Header` to the intended route target