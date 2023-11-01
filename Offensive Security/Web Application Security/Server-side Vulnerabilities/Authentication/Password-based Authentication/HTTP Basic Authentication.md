HTTP basic authentication is still used due to its simplicity and ease of implementation. Here, the client receives an authentication token from the server by combining the username and password, then encoding it in Base64.

The token is stored and managed by the browser, automatically adding it to the `Authorization` header of each subsequent request in the format `Authorization: Basic base64(username:password)`. Unless the website implements HTTP Strict Transport Security (HSTS), user credentials will be captured by a man-in-the-middle attack.

In addition, HTTP Basic Authentication often don't support brute force protection. As the token consists exclusively of static values, this can leave it vulnerable to being brute-forced.

<!-- @TODO: Link CSRF from Client-side Vulnerabilities -->
Additionally, it is also particularly vulnerable to session-related exploits, notably Cross-Site Request Forgery (CSRF).