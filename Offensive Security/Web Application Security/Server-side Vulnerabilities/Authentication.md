Conceptually, authentication vulnerabilities are easy to understand. However, they are usually critical because of the clear relationship between authentication and security.

Authentication vulnerabilities can allow attackers to gain access to sensitive data and functionality. They also expose additional attack surface for further exploits. For this reason, it's important to learn how to identify and exploit authentication vulnerabilities, and how to bypass common protection measures.
## Authentication vs Authorization
Authentication is the process of verifying that a user is who they claim to be. Authorization involves verifying whether a user is allowed to do something.

For example, authentication determines whether someone attempting to access a website with the username `carlos` is really the same person who created the account.

Once `carlos` has been authenticated, their permissions will determine what they are authorized to do, such as accessing or modifying another user's personal information.
## Brute Force Attacks
A brute force attack is an attack when an attacker uses a system of trial and error to guess valid user credentials. These attacks are typically automated using wordlists of usernames and passwords, and using dedicated tools, enabling the attacker to make vast numbers of login attempts at high speed.

Brute forcing is not always a case of complete random guesses at usernames and passwords. Attackers can also take advantage of basic logic or publicly available knowledge to fine-tune brute force attacks to make a much more educated guesses which increases the efficiency of the attack.

Websites relying on password-based login as their sole method of authenticating users can be highly vulnerable if they do not implement sufficient brute-force protection such as maximum login attempts and rate limits.
### Brute Forcing Usernames
Usernames are specially easy to guess if they confirm to a recognizable pattern, such as an email address. For example, it is very common for businesses to implement email address formats for their employees - `firstname.lastname@company.com`. However, even if there is no obvious patterns, some high-privileged accounts are created to use predictable usernames such as `admin` or `administrator`.

During audit, it is important to check whether the website discloses potential usernames publicly. For example, an attacker can access user profiles without logging in due to a [broken access control](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FAccess%20Control). Even if the actual content of the profile is hidden, the name used in the profile is sometimes used as the login username. It is also worthwhile to check HTTP responses to see if any email addresses are disclosed, as this can occasionally contain email addresses of high-privileged users, such as administrators or IT support.
### Brute Forcing Passwords
Passwords can be similarly brute forced, with difficulty varying based on the strength of the password. Many website adopt some form of password policy, which forces their users to create high entropy passwords that are harder to crack using brute force alone, theoretically. This typically involves:
- Minimum number of characters
- Mixture of upper and lowercases letters
- At least one special character

However, while high entropy passwords are difficult for computers alone to crack, we can use basic knowledge of human behavior to exploit the vulnerabilities that users introduce to the system. For example, rather than following the password policy and creating strong passwords, users will often take a password they can remember and try to crowbar it into fitting the password policy. For example, if `mypassword` is not allowed, users may try something like `Mypassword1!` or `Myp4$$w0rd` instead.

In cases where the policy requires users to change their passwords every now and then, it is also common for users to do minor or predictable changes such as changing `Mypassword!` to `Mypassword!?`.
## Username Enumeration
Username enumeration is when an attacker is able to observe changes in the website's behavior in order to identify whether a given username is valid. This typically occurs either on the login or registration page, when the error message gives hint to the attacker such as:
- Username is already taken
- Incorrect Password

This greatly reduces the time and effort required to do a brute force attack because the attacker can quickly generate a shortlist of valid usernames.

While attempting to brute force a login page, we should also pay particular attention to any differences in:
- Status Code - Most of the time, the returned HTTP status code is likely to be the same for the vast majority of guesses because most of them will be wrong. If a guess returns a different status code, this is a strong indication that the username was correct.
- Error Messages - Sometimes the returned error message is different depending on whether both the username and password are incorrect or only the password was incorrect.
- Response Times - If most of the requests were handler with a similar response time, any difference from this suggests that something different was happening behind the scenes. This is another indication that the guessed username might be correct.
## Bypassing Two-Factor Authentication
At times, the implementation of 2FA is flawed to the point where it can be bypassed entirely.

If the user is first prompted to enter a password, and then prompted to enter a verification code on a separate page, the user is effectively in a "logged in" state before they have entered the verification code. In this case, it is worst testing to see if you can directly skip the "logged-in only" pages. Occasionally, websites doesn't actually check whether or not the user has completed the second step before loading a different page.