Some applications do not maintain any server-side record of tokens that have been issued, instead they duplicate each token within a cookie and a request parameter.

This works by having the application verify the token submitted in the request matches the value of the cookie. This is sometimes called the "double submit" defense against CSRF, which is a simple mechanism that avoids the need for any server-side state. For example:
```http
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=1DQGdzYbOJQzLP7460tfyiv3do7MjyPw; csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa

csrf=R8ov2YBfTYmzFyjit8o2hKBuoIjXXVpa&email=wiener@normal-user.com
```
In this situation, the attacker can simply look for and abuse any cookie setting functionality wherein they will put the same token in both the cookie and request parameter. They can also simply invent a token of their own (following the required format, if the application checks for it).