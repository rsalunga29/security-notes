The default behavior of CORS requests is for requests to be passed without credentials like cookies and the Authorization header. However, using the `Access-Control-Allow-Credentials` and setting it to `true`, credentials to be included in the cross-origin request.

For example, this requesting website uses JavaScript to declare that it is sending cookies with the request:
```http
GET /auth/accountDetails HTTP/1.1
Host: robust-website.com
...
Origin: https://normal-website.com
Cookie: JSESSIONID=<value>
```
And if the response is:
```http
HTTP/1.1 200 OK
...
Access-Control-Allow-Origin: https://normal-website.com
Access-Control-Allow-Credentials: true
```
The browser will permit the requesting website to pass credentials and read the response. Otherwise, the browser will not allow access to the response.