Also known as CSRF, is a web security vulnerability that allows an attacker to partly circumvent the [Same-origin Policy](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Origin%20Resource%20Sharing%20(CORS)%2FSame-origin%20Policy%2FIntroduction) and forces an authenticated end-user to perform unintended actions. This attack is usually mounted with the help of attacker-crafted web pages that the victim must visit or interact with, leveraging the lack of anti-CSRF security mechanisms.

These web pages contain malicious requests that inherit the identity and privileges of the victim to perform unintended actions on the victim's behalf. CSRF attacks generally target functions that cause a state change on the server but can also be used to access sensitive data.

A web application is vulnerable to CSRF attacks when:
- All the parameters required for the targeted request can be determined or guessed by the attacker.
- The application's session management is solely based on HTTP cookies, which are automatically included in browser requests.

To successfully exploit a CSRF vulnerability, we need:
- To craft a malicious web page that will issue a valid (cross-site) request impersonating the victim.
- The victim to be logged into the application at the time when the malicious cross-site request is issued.

CSRF attacks are typically delivered the same way as reflected [XSS](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FIntroduction), wherein the attacker will place the malicious HTML onto a website that they control and induce the victims to visit that website. This might be done by feeding the user a link to the website, via email or social media message, or placing it into a popular website, in which case the attacker would just wait for users to visit the website.

Depending on the nature of the CSRF attack, the attacker might be able to gain full control over a user's account. If the compromised user has a privileged role, the attacker might even be able to take full control of all of application's data and functionality.
> Note: In your web application penetration testing or bug bounty hunting endeavors, you will notice a lot of applications that feature no anti-CSRF protections or anti-CSRF protections that can be easily bypassed.