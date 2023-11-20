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
## Example Exploit
Imagine a shopping application that allows its users to change their email address and search for products within the store.

1. Login to your account. Submit the "Update email" form and intercept the request using Burp Proxy, then send the request to Burp Repeater.
2. In Burp Repeater, observe that changing the `session` cookie logs you out, but changing the `csrfKey` cookie merely results in the token being rejected, which may suggest that `csrfKey` cookie may not be strictly tied to the session.
3. Open incognito window and login to your another account, submit the "Update email" and send it to Burp Repeater.
4. Observe that if you swap the `csrfKey` cookie and `csrf` parameter from the first account to the second account, the request is accepted.
5. Back to the browser, perform a search and send the resulting request in Burp Repeater. Observe that the search term gets reflected in the `Set-Cookie` response header.
6. Confirm the search parameter is vulnerable to [CRLF Injection](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FCRLF%20Injection%2FIntroduction) by using the following value:
```txt
/?search=test%0d%0aSet-Cookie:%20csrfKey=uM3IBWr9qbdJgnV9DBqjXEOcdHG3rMPp%3b%20SameSite=None
```
7. Use the following payload for the attack
```html
<form action="https://vulnerable-website.com/my-account/change-email" method="post">
	<input type="hidden" name="email" value="pwned@normal-user.net" />
	<input type="hidden" name="csrf" value="fh6RhHzKaIRlyk2fzZJW1Xxxj6KVpDZp" />
</form>

<img src="https://vulnerable-website.com/?search=test%0d%0aSet-Cookie:%20csrf=uM3IBWr9qbdJgnV9DBqjXEOcdHG3rMPp%3b%20SameSite=None" onerror="document.forms[0].submit()">
```
8. Store the exploit then click "Deliver to victim" to solve the lab.
## Note
The cookie-setting behavior does not even need to exist within the same web application as the CSRF vulnerability. Any other application within the same overall DNS domain can be leveraged to set cookies in the application that is being targeted, this attack is called [cookie tossing](https://book.hacktricks.xyz/pentesting-web/hacking-with-cookies/cookie-tossing). For example, a cookie-setting function on `staging.demo.normal-website.com` could be leveraged to place a cookie that is submitted to `secure.normal-website.com`.