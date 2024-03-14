Passwords can be similarly brute forced, with difficulty varying based on the strength of the password. Many website adopt some form of password policy, which forces their users to create high entropy passwords that are harder to crack using brute force alone, theoretically. This typically involves:
- Minimum number of characters
- Mixture of upper and lowercases letters
- At least one special character

However, while high entropy passwords are difficult for computers alone to crack, we can use basic knowledge of human behavior to exploit the vulnerabilities that users introduce to the system. For example, rather than following the password policy and creating strong passwords, users will often take a password they can remember and try to crowbar it into fitting the password policy. For example, if `mypassword` is not allowed, users may try something like `Mypassword1!` or `Myp4$$w0rd` instead.

In cases where the policy requires users to change their passwords every now and then, it is also common for users to do minor or predictable changes such as changing `Mypassword!` to `Mypassword!?`.
## Password Policy Deduction
The chances of executing a successful brute force attack increase after a proper policy evaluation. Knowing what the minimum password requirements are, allows an attacker to start testing only compliant passwords. On virtually any application that allows self-registration, it is possible to evaluate the password policy by registering a new user. Trying to use the username as a password, or a very weak password like `123456`, often results in an error that will reveal the policy (or some parts of it) in a human-readable format.

However, during a real engagement, it is possible that an application only replies with a "Password does not meet complexity requirements" message. This will then become a guessing game, we can start guessing the requirements by entering a keyboard walk sequence for the password like `Qwertyiop123!@#`, which is actually predictable, but it is long and complex enough to match standard policies. Should the application accepts such passwords as valid. We can start decreasing the complexity by removing special characters, then numbers, then uppercase characters, and eventually decreasing the length by one character at a time. Within a few tries, we should be able to identify the policy requirements and we can now create a matrix with the minimum requirements.

It is also possible that an application only replies a generic error message at first and reveals exact policy conditions after a number of failed attempts. This is why it is recommended to test three or four times before giving up.
### Modifying Wordlist based on Policy
Now that the attacker knows the minimum password requirements, they can now take a giant wordlist and extract only passwords that match the target's policy. Unix `grep` is not the fastest tool but allows us to do the job quickly using POSIX regular expressions. For example:
```bash
grep '[[:upper:]]' rockyou.txt | grep '[[:lower:]]' | grep -E '^.{8,12}$' | wc -l

416712
```
This command finds lines have at least one uppercase character (`'[[:upper:]]'`), and then only lines that also have a lowercase one (`'[[:lower:]]'`) and with a length of 8 and 12 chars ('^.{8,12}$') using extended regular expressions (-E).

We see that starting from the standard `rockyou.txt`, which contains more than 14 million lines, we have narrowed it down to roughly 400 thousand.