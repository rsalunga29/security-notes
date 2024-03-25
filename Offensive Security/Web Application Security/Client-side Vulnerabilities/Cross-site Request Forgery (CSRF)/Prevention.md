## SameSite Flag
The SameSite flag allows developers declare whether a cookie is restricted to first-party or same-site context only. The main goal is to mitigate the risk of cross-origin information leakage. It also provides some protection against cross-site request forgery attacks.

The SameSite flag may have one of the following values:
- `SameSite=Strict`: The cookie is only sent if you are currently on the site that the cookie is set for. If you are on a different site and you click a link to a site that the cookie is set for, the cookie is _not_ sent with the first request.
- `SameSite=Lax`: The cookie is _not_ sent for embedded content but it _is_ sent if you click on a link to a site that the cookie is set for. It is sent only with safe request types that do not change state, for example, GET.
- `SameSite=None`: The cookie is sent even for embedded content.

For example:
```http
Set-Cookie: sessionid=QmFieWxvbiA1; HttpOnly; Secure; SameSite=Strict
```