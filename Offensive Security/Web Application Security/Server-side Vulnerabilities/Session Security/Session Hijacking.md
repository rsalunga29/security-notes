In session hijacking attacks, the attacker takes advantage of insecure session identifiers, finds a way to obtain them, and uses them to authenticate to the server and impersonate the victim.

An attacker can obtain a victim's session identifier using several methods, with the most common being:
- Passive Traffic Sniffing
- Cross-Site Scripting (XSS)
- Browser history or log-diving
- Read access to a database containing session information

Additionally, if the randomness of session IDs is weak, an attacker may be able to brute force it or even predict it.
## Example
1. Navigate to `http://target-website.com/` and login using the default credentials.
2. Once logged in, open the browser developer tools and notice that the application is using a cookie named `auth-session`, which is most probably a session ID. Copy the cookie value.
3. Open a new private window and navigate to the same website.
4. Open the browser developer tools, if the cookie named `auth-session` already exists, replace the value with the one we copy-pasted in step 2. Otherwise, create a new cookie using the same name and value.
5. Notice that we are able to access someone else's personal page without logging in.