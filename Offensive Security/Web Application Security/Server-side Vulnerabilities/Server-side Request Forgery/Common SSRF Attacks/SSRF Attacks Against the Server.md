In an SSRF attack against the server, the attacker causes the application to make an HTTP request back to the server that is hosting the application. This typically involves supplying a URL hostname like `127.0.0.1` or `localhost`.

For example, imagine a shopping application that lets a user view whether an item is in stock in a particular store branch. To do this, the application passes a URL to the relevant backend API endpoint via a HTTP request:
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```
This causes the server to make a request to the specified URL, retrieve the information, and return the results to the user.

In this example, an attacker can modify the request body to fetch the contents of the `/admin` URL instead.
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```
This will result in the attacker gaining access to an internal-only admin application. While the attacker won't see anything of interest yet, as the critical functionality is hidden behind an authentication, the [normal access controls](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FAccess%20Control%2FIntroduction) are still bypassed as the request originated from the local machine, which is a trusted location.