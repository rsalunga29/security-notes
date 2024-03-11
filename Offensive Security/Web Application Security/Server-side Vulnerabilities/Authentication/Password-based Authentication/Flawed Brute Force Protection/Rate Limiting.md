Another way to try to prevent brute force attacks is through user rate limiting. In this case, making too many login requests within a short period of time causes your IP address to be blocked. However, the IP can be unblocked in one of the following ways:
- Automatically after a certain period of time has elapsed.
- Manually by an administrator.
- Manually by the user after successfully completing a CAPTCHA.
- Manually crafting the HTTP Header Request to add `X-Forwarded-For` to fool the rate-limiting mechanism.

User rate limiting is sometimes preferred to account locking due to being less prone to username enumeration and denial of service attacks. However, an attacker can [manipulate their apparent IP in order to bypass this](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FAuthentication%2FPassword-based%20Authentication%2FFlawed%20Brute%20Force%20Protection%2FIP%20Blocking).
## Exploit via Multiple Credentials per Request
This might only work if the request is being submitted as a JSON format.
1. Investigate the login request. If it's submitting login credentials in JSON format. Send the request to Burp Repeater.
2. In Burp Repeater, replace the single string value of the password with an array of strings containing potential passwords, for example:
```json
"username" : "carlos",
"password" : [
	"123456",
	"password",
	"qwerty"
	...
]
```
3. Send the request. When finished, look for a `302` response.
4. Right-click on the request and select **Show response in browser**. Copy the URL and load it in the browser.
## Anti-Rate Limit Custom Script
We can also create a custom Python script to overcome rate limiting, by teaching our tool to understand messages related to rate-limiting and we can, for example, tell our tool to "sleep" for x seconds to wait for the cooling-off period to pass before trying again. Although this can only work when the rate-limiting mechanism applies a cooling-off period.