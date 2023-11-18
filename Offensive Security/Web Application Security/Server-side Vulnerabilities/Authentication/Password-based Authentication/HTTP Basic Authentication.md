HTTP basic authentication is still used due to its simplicity and ease of implementation. Here, the client receives an authentication token from the server by combining the username and password, then encoding it in Base64.

The token is stored and managed by the browser, automatically adding it to the `Authorization` header of each subsequent request in the format `Authorization: Basic base64(username:password)`. Unless the website implements HTTP Strict Transport Security (HSTS), user credentials will be captured by a man-in-the-middle attack.

In addition, HTTP Basic Authentication often don't support brute force protection. As the token consists exclusively of static values, this can leave it vulnerable to being brute-forced.

Additionally, it is also particularly vulnerable to session-related exploits, notably [Cross-Site Request Forgery (CSRF)](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-site%20Request%20Forgery%20(CSRF)%2FIntroduction).