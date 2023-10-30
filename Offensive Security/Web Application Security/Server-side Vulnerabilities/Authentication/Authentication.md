Conceptually, authentication vulnerabilities are easy to understand. However, they are usually critical because of the clear relationship between authentication and security.

Authentication vulnerabilities can allow attackers to gain access to sensitive data and functionality. They also expose additional attack surface for further exploits. For this reason, it's important to learn how to identify and exploit authentication vulnerabilities, and how to bypass common protection measures.
## Authentication vs Authorization
Authentication is the process of verifying that a user is who they claim to be. Authorization involves verifying whether a user is allowed to do something.

For example, authentication determines whether someone attempting to access a website with the username `carlos` is really the same person who created the account.

Once `carlos` has been authenticated, their permissions will determine what they are authorized to do, such as accessing or modifying another user's personal information.
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