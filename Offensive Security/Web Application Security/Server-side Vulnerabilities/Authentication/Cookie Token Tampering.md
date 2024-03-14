Most tokens are sent and received using cookies. Therefore, cookie security should always be checked.

There will be times where session tokens/cookies can be based on guessable information. Often, homebrewed web applications feature custom session handling and custom cookie-building mechanisms to have user-related details handy. The most common piece of data we can find in cookies are user id, grants, time, etc. Let us consider the following example:
![[cookie-tampering.png]]
Line 4 of the server’s response shows a `Set-Cookie` header that sets a `SESSIONID` to `757365723A6874623B726F6C653A75736572`. If we decode this hex value as ASCII, we see that it contains our `userid`, `htb`, and role (standard `user`).
```bash
echo -n 757365723A6874623B726F6C653A75736572 | xxd -r -p; echo

user:htb;role:user
```
We could try escalating our privileges within the application by modifying the `SESSIONID` cookie to contain `role:admin`. This action may even allow us to bypass authentication altogether.

Finally, cookies should be created with the correct path value, be set as `httponly` and `secure`, and have the proper domain scope. An unsecured cookie could be stolen and reused quite easily through Cross-Site Scripting (XSS) or Man in the Middle (MitM) attacks.