Passwords can be similarly brute forced, with difficulty varying based on the strength of the password. Many website adopt some form of password policy, which forces their users to create high entropy passwords that are harder to crack using brute force alone, theoretically. This typically involves:
- Minimum number of characters
- Mixture of upper and lowercases letters
- At least one special character

However, while high entropy passwords are difficult for computers alone to crack, we can use basic knowledge of human behavior to exploit the vulnerabilities that users introduce to the system. For example, rather than following the password policy and creating strong passwords, users will often take a password they can remember and try to crowbar it into fitting the password policy. For example, if `mypassword` is not allowed, users may try something like `Mypassword1!` or `Myp4$$w0rd` instead.

In cases where the policy requires users to change their passwords every now and then, it is also common for users to do minor or predictable changes such as changing `Mypassword!` to `Mypassword!?`.
## Password Policy Deduction
The chances of executing a successful brute force attack increase after a proper policy evaluation. Knowing what the minimum password requirements are, allows an attacker to start testing only compliant passwords. On virtually any application that allows self-registration, it is possible to infer the password policy by registering a new user. Trying to use the username as a password, or a very weak password like `123456`, often results in an error that will reveal the policy (or some parts of it) in a human-readable format.