Insecure web server configurations cause the first type of HTTP Verb Tampering vulnerabilities. A web server's authentication configuration may be limited to specific HTTP methods, which would leave some HTTP methods accessible without authentication.

For example, the following configuration is used to require authentication on a particular page:
```xml
<Limit GET POST>
	Require valid-user
</Limit>
```
If an attacker uses a HTTP method (e.g `PUT`), they will be able to bypass this authentication mechanism altogether.