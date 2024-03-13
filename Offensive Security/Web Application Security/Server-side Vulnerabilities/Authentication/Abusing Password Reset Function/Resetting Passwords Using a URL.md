An even better method of resetting passwords is to send a unique URL to users that takes them to a password reset page. However, some less secure implementation of this methods do exists, such as using a predictable URL parameter to identify which account is being reset, for example:
```txt
https://target-website.com/password-reset?user=bob
```
In this example, the attacker could change the `user` parameter to a username of the account they are targeting, where they would be taken to the password reset page and set a new password for the target user.

A better implementation of this process is to generate a high-entropy, hard-to-guess token and create the reset URL from that. For example:
```txt
https://target-website.com/password-reset?token=a0ba0d1cb3b63d13822572fcff1a241895d893f659164d4cc550b421ebdd48a8
```
When the user visits the URL, the system should check the token's existence and validity. If confirmed, it should identify the associated user for password reset. This token should expire after a short period of time and be destroyed immediately to prevent it from being reused.

However, some web applications uses predictable tokens or they 

fails to validate the token again when the reset form is submitted. In this case, an attacker could delete the token and reset another user's account.

<!--- @TODO: Link Password Reset Poisoning from HTTP Host header attacks section -->
Even if the URL in the reset email is generated dynamically, it may still be vulnerable to password reset poisoning. In this case, an attacker can potentially steal another user's token and use it to change their password.
## Example Exploit for Broken Password Reset Logic
1. With Burp Proxy, capture the `POST /forgot-password?token=` request and send it to Burp Repeater.
2. In Burp Repeater, observe that the password reset still works even if you delete the value of `token` parameter in both the URL and request body. This confirms that the token is not being checked when you submit a new password.
3. Delete the value of `token` parameter in both the URL and request body. Change the `username` parameter to `carlos`. Set the new password to whatever you want.
4. Send the request. Access `carlos` account using the new password.