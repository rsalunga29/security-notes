It should go without saying that sending users their current password should never be possible if a website handles passwords securely in the first place. Instead, it is better to generate a new password and send this to the user via email.

However, sending persistent passwords over insecure channels must be avoided. In this case, the security relies on either the generated password expiring after a very short period, or the user changing their password again immediately. Otherwise, this approach is highly susceptible to man-in-the-middle attacks.

Email is also generally not considered secure due to the fact that inboxes are both persistent and not really designed for secure storage of confidential information. Many users also automatically sync their inboxes across insecure channels.