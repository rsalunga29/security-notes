In some cases, the application server is able to interact with backend systems that are not reachable by users, due to having a non-routable private IP addresses. In many cases, internal backend systems contain sensitive functionalities that can be accessed without authentication.

In the [previous example](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FServer-side%20Request%20Forgery%2FCommon%20SSRF%20Attacks%2FSSRF%20Attacks%20Against%20the%20Server), imagine there is an administrative interface at the backend URL `https://192.168.0.68/admin`. An attacker can submit the following request to exploit the SSRF vulnerability and access the admin interface:
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=https://192.168.0.68/admin
```
