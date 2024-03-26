SameSite is a browser security mechanism that enables browsers and website owners to limit which cross-site requests should include specific cookies. It also provides partial protection against cross-site attacks, such as CSRF, cross-site information leakage, and some [CORS](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Origin%20Resource%20Sharing%20(CORS)%2FIntroduction) exploits.

All major browsers currently support the following SameSite restriction levels:
- **Strict** - The most restrictive option. The browser sends the cookie only for same-site requests, that is, requests originating from the same site that set the cookie.
- **Lax** - Since 2021, Chrome sets `Lax` as the default value if the website that issues the cookie doesn't explicitly sets its own restriction level. The browser does not send the cookie on cross-site requests, such as on requests to load images or frames, but is sent when a user is navigating to the origin site from an external site (i.e following a link).
- **None** - Removes any same-site requirements from the cookie. However, the cookie must be marked as Secure (i.e `SameSite=None; Secure`), otherwise an error will be logged. The browser sends the cookie on both cross-site and same-site requests.

*Note: Developers can manually configure a restriction level for each cookie they set, giving them more control over when these cookies are used.* To do this, they just have to include the `SameSite` attribute in the `Set-Cookie` response header (i.e `Set-Cookie: session=abc123; SameSite=Strict`).
## Context of "site" in SameSite Cookies
In the context of SameSite cookie restrictions, a site is defined as the top-level domain (TLD), plus one additional level of domain name, defined as TLD+1. For example, the `example.com` from `https://app.example.com` is considered as TLD+1.

When SameSite determines whether a request is same-site or not, the URL scheme is also taken into consideration. This means that a link from `http://app.example.com` to `https://app.example.com` is treated as cross-site by most browsers.