Although fairly old, its relative simplicity and ease of implementation means you might sometimes see HTTP basic authentication being used. In HTTP basic authentication, the client receives an authentication token from the server, which is constructed by concatenating the username and password, and encoding it in Base64. This token is stored and managed by the browser, which automatically adds it to the `Authorization` header of every subsequent request as follows: `Authorization: Basic base64(username:password)`.

This is not generally considered a secure authentication method. As it repeatedly sends the user's login credentials with every request. Unless the website implements HTTP Strict Transport Security (HSTS), user credentials will be captured by a man-in-the-middle attack.

In addition, HTTP Basic Authentication often don't support brute force protection. As the token consists exclusively of static values, this can leave it vulnerable to being brute-forced.

Additionally, it is also particularly vulnerable to session-related exploits, notably Cross-Site Request Forgery (CSRF).