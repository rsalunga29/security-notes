Depending on the implementation of this brute force protection, you can bypass it by either using `X-Forwarded-For` HTTP header or by successfully logging in to your account to reset the failed login attempts counter.
## X-Forwarded-For HTTP Header
1. In Burp Intruder, add the `X-Forwarded-For` on the HTTP request, this allows you to spoof your IP address.
2. Add payload positions to the value of `X-Forwarded-For`. On the **Payloads** tab, select the **Numbers** payload type. Enter the range 1 - 100 and set the step to 1. Set the max fraction digits to 0.
3. Start the attack. When finished, look for a `302` HTTP response.
> Note: Alternatively, we can just set a static `X-Forwarded-For: 127.0.0.1` instead.
## Reset Failed Login Attempts Counter by Successfully Logging In
1. In Burp Intruder, select the **Resource pool** tab then add the attack to a resource pool with **Maximum concurrent requests** set to `1`. By only sending one request at a time, you can ensure that your login attempts are sent over to the server in the correct order.
2. On the **Payloads** tab, add a username wordlist that alternates between your username and the target username. Make sure that your username is first and then the target username. This should be repeated at least 100 times.
3. Add a password wordlist and add your own password before each one. Make sure that your password is aligned with your username in the other wordlist.
4. Start the attack. When finished, look for a `302` HTTP response.