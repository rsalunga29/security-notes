The default behavior of CORS requests is for requests to be passed without credentials like cookies and the Authorization header. However, when `Access-Control-Allow-Credentials` is set to true, the cross-domain server can permit the reading of the response.

For example, this requesting website uses JavaScript to declare that it is sending cookies with the request:
```http
GET /data HTTP/1.1
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
The browser will permit the requesting website to read the response. Otherwise, the browser will not allow access to the response.