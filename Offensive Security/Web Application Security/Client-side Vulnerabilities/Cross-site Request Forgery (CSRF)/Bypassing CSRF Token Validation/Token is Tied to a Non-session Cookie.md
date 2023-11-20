Some applications tie the CSRF token to a cookie, but not to the same cookie that is used to track sessions. This usually occurs when an application uses two different frameworks, one for session handling and one for CSRF protection, which are not integrated together. For example:
```http
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 68
Cookie: session=pSJYSScWKpmC60LpFOAHKixuFuM4uXWF; csrfKey=rZHCnSzEp8dbI6atzagGoSYyqJqTz5dv

csrf=RhV7yQDO0xcq9gLEah2WVbmuFqyOq7tY&email=wiener@normal-user.com
```
This situation is normally harder to exploit, since an attack is only possible if the website contains any behavior that allows an attacker to set a cookie in the victim's browser. In this case, an attacker can obtain a valid CSRF and session token from their own account, leverage a cookie-setting behavior to inject their cookie into the victim's browser and conduct an attack.