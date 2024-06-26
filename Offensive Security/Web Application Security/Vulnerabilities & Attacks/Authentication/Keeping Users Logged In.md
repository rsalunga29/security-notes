A common feature is the option to stay logged in even after closing a browser session. This is usually a simple checkbox labeled as "Remember me" or "Keep me logged in".

This is often implemented by generating a "remember me" token, which is then stored in as a persistent cookie. As possessing this cookie allows you to bypass the entire login process, it is best practice for this cookie to be impractical to guess. However, some websites generate this cookie based on a predictable concatenation of static values (e.g username and timestamp). Even worst, some even use the password as part of the cookie.

This approach is particularly dangerous specially if the attacker can create their own account and study their own cookie and potentially deduce how it is generated and brute force other user's cookies.

Even without creating an account, they may still exploit this vulnerability with Cross Site Scripting (XSS) to steal "remember me" cookies and deduce how the cookie is generated. If the website is using an open-source framework, the key details of the cookie construction may even be publicly documented.

In rare cases, a user's plaintext password may be obtained from a cookie, even if it's hashed. Online hashed password lists make decryption easy for common passwords.
## Exploit Example
1. With Burp running, login to your own account with the **Stay logged in** option selected. Notice that this sets a `stay-logged-in` cookie.
2. Examine the cookie and notice that is it Base64-encoded. It's decoded value is `wiener:51dc30ddc473d43a6011e9ebba6ca770`. Notice that the length and character set of this string could be an MD5 hash. Given that the plaintext is your username, you can make an educated guess that this may be your password.
3. Notice that the cookie is constructed as follows `base64(username+':'+md5HashOfPassword)`
4. Log out of your account.
5. In the most recent `GET /my-account`, highlight the `stay-logged-in` cookie parameter and send the request to Burp Intruder.
6. Use [Payload processing](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FBurp%20Suite%20Tips%20%26%20Tricks%2FBurp%20Intruder%20Payload%20Processing) to process the cookie based on how its constructed.
7. As the `Your account name is: target-username` is only displayed when you access the `/my-account` page in an authenticated state, we can use the presence or absence of this text to determine whether we've successfully brute forced the cookie. On the **Settings** tab, add a grep match rule to flag any responses containing the text.
8. Start the attack.