One way in which websites try to prevent brute-forcing is to lock the account if certain suspicious criteria are met, usually a set number of failed login attempts. Just as with normal login errors, responses from the server indicating that an account is locked can also help an attacker to enumerate usernames.

However, this approach fails adequately to prevent brute force attacks in which the attacker is just trying to gain access to any random account they can.

For example, the following method can be used to work around this kind of protection:
1. Establish a list of candidate usernames that are likely to be valid. This could be through username enumeration or simply based on a list of common usernames.
2. Decide on a very small shortlist of passwords that you think at least one user is likely to have. The number of passwords you select must not exceed the number of login attempts allowed. For example, if you have worked out that limit is 3 attempts, you need to pick a maximum of 3 password guesses.
3. Using a tool, try each of the selected passwords with each of the usernames. This way, you can attempt to brute-force every account without triggering the account lock.

Account locking also fails to protect against credential stuffing attacks. This involves using a massive dictionary of `username:password` pairs, composed of genuine login credentials stolen in data breaches. Credential stuffing relies on the fact that many people reuse the same username and password on multiple websites and, therefore, there is a chance that some of the compromised credentials in the dictionary are also valid on the target website.
## Exploit Using Burp Suite
1. In Burp Intruder, add payload positions to the `username` parameter and at the end of the request body. The result should look something like this: `username=§invalid-username§&password=example§§`
2. On the **Payloads** tab, add a list of usernames to the first payload set. For the second set, select **Null payloads** type and choose the option to generate 5 payloads. This will effectively cause each username to be repeated 5 times.
3. Start the attack. When finished, look for an error message that may indicate the account has been locked due to incorrect login attempts. Make note of this username.
4. Brute force for the password of the username.