SameSite is a browser security mechanism that determines when a website's cookies are included in requests originating from other websites. It also provides partial protection against cross-site attacks, such as CSRF, cross-site leaks, and some [CORS](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Origin%20Resource%20Sharing%20(CORS)%2FIntroduction) exploits.

SameSite have three values passed into it. These are:
- **Strict**
- **Lax** - Since 2021, Chrome sets `Lax` as the default value if the website that issues the cookie doesn't explicitly sets its own restriction level.
- **None**

Since 2021, Chrome sets `Lax` as SameSite's default value if the website that issues the cookie doesn't explicitly sets its own restriction level. Other values available are: `Strict` and `None`.