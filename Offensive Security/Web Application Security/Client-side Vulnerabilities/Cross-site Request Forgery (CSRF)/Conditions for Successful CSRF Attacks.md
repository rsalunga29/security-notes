For a CSRF attack to be possible, three key conditions must be in place:
1. **A relevant action.** There is an action within the application that the attacker has a reason to induce, this might be a privileged action (such as modifying or deleting user data) or any action on user-specific data (such as changing password).
2. **Cookie-based session handling.** The action involves invoking HTTP request and must solely rely on session cookies to identify the user who has made the request. There must also be no other mechanism in place for tracking or validating session tokens used in the user's request.
3. **No unpredictable request parameters.** The request that performs the action must not contain any parameters that an attacker cannot determine or guess. For example, during password change functionality, it will not be vulnerable if the attacker needs to know the value of the existing password.

For example, the following request meets all the conditions required for a CSRF attack to take place:
```http
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```
With the required conditions in place, the attacker can construct the following web page:
```html
<html>
    <body>
        <form action="https://vulnerable-website.com/email/change" method="POST">
            <input type="hidden" name="email" value="pwned@evil-user.net" />
        </form>
        <script>
            document.forms[0].submit();
        </script>
    </body>
</html>
```
If a victim user visits this web page, the following will happen:
- The attacker's page will trigger an HTTP request to the vulnerable web site.
- If the user is logged in to the vulnerable web site, their browser will automatically include their session cookie in the request (assuming [SameSite cookies](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-site%20Request%20Forgery%20(CSRF)%2FCommon%20CSRF%20Defenses) are not being used).
- The vulnerable web site will process the request in the normal way, treat it as having been made by the victim user, and change their email address.