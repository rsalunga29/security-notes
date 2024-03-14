Brute force protection revolves around trying to make it as tricky as possible to automate the process and slow down the rate at which an attacker can attempt logins. The two most common ways of preventing brute force attacks are:
- Locking the account that the remote user is trying to access if they make too many failed login attempts
- Blocking the remote user's IP address if they make too many login attempts in quick succession

Both approaches offer varying degrees of protection, but neither is invulnerable, especially if implemented using flawed logic.

For example, in the case of blocking an IP after repeated failed logins, the counter resets if the IP owner logs in successfully. This allows the attacker to bypass the limit by logging into their own account intermittently.