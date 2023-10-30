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