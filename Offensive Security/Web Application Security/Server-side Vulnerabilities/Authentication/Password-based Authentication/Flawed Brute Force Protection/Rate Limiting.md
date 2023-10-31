Another way to try to prevent brute force attacks is through user rate limiting. In this case, making too many login requests within a short period of time causes your IP address to be blocked. However, the IP can be unblocked in one of the following ways:
- Automatically after a certain period of time has elapsed
- Manually by an administrator
- Manually by the user after successfully completing a CAPTCHA

User rate limiting is sometimes preferred to account locking due to being less prone to username enumeration and denial of service attacks. However, an attacker can [manipulate their apparent IP in order to bypass this](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FAuthentication%2FPassword-based%20Authentication%2FFlawed%20Brute%20Force%20Protection%2FIP%20Blocking).