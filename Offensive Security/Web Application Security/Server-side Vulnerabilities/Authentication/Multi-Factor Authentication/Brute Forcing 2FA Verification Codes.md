As with passwords, websites need to take steps to prevent brute forcing of the 2FA verification code. This is essentially important because the code is often a simple 4 or 6-digit number. Without adequate brute force protection, cracking such a code is trivial.

Some websites attempt to prevent this by automatically logging a user out if they enter a certain number of incorrect verification codes. This is ineffective in practice because an advanced attacker can even automate this multi-step process by creating macros for Burp Intruder, and/or using the Turbo Intruder extension.
## Example Exploit
In this example, we already have the username and password of our target user, but we still need the 2FA verification code. However, if we enter the wrong code an x amount of times, the website will force us to logout.
1. In Burp, we need to create a macro to bypass