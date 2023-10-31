Username enumeration is when an attacker is able to observe changes in the website's behavior in order to identify whether a given username is valid. This typically occurs either on the login or registration page, when the error message gives hint to the attacker such as:
- Username is already taken
- Incorrect Password

This greatly reduces the time and effort required to do a brute force attack because the attacker can quickly generate a shortlist of valid usernames.

While attempting to brute force a login page, we should also pay particular attention to any differences in:
- Status Code - Most of the time, the returned HTTP status code is likely to be the same for the vast majority of guesses because most of them will be wrong. If a guess returns a different status code, this is a strong indication that the username was correct.
- Error Messages - Sometimes the returned error message is different depending on whether both the username and password are incorrect or only the password was incorrect.
- Response Times - If most of the requests were handler with a similar response time, any difference from this suggests that something different was happening behind the scenes. This is another indication that the guessed username might be correct.