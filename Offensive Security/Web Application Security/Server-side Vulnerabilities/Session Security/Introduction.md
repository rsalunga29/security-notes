A user session can be defined as a sequence of requests originating from the same client and the associated responses during a specific time period. Modern web applications utilize user sessions to facilitate the assignment of access or authorization rights, localization settings, etc.

Since HTTP is a stateless communication protocol, each requests only carry enough information for the server to act upon it. This means that session state can only reside on the client side.

For this reason, web applications utilizes cookies, URL parameters, URL arguments (on GET requests), body arguments (on POST requests), and other proprietary solutions for session tracking and management purposes.
## Session Identifier Security
A unique session identifier (Session ID) or token is the basis upon which user sessions are generated and distinguished.

A session identifier's security level depends on its:
- Validity Scope - a secure session identifier should be valid for one session only.
- Randomness - a secure session identifier should be generated through a robust random number/string generation algorithm so that it cannot be predicted.
- Validity Time - a secure session identifier should expire after a certain amount of time.

A session identifier's security level also depends on the location where it is stored:
- URL - The HTTP Referer header can leak the session ID to other websites. It will also be recorded on the browser history.
- HTML - The session ID can be identified in both the browser's cache memory or any intermediate proxies.
- `sessionStorage` -  The `sessionStorage` is a browser-based storage feature introduced in HTML5. Session IDs stored in this location can be retrieved via the browser developer tools. However, `sessionStorage` gets cleared when the tab or browser is closed.
- `localStorage` - The `localStoage` is a browser-based storage feature introduced in HTML5.  Session IDs stored in this location can be retrieved via the browser developer tools. Additionally, `localStorage` values will persists so long as the `localStorage` does not get deleted by the user.
> Note: Session identifiers that are managed with no server interference or that do not follow the secure "characteristics" above should be reported as weak.