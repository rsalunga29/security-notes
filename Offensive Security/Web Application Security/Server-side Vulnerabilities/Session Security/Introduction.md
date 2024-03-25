A user session can be defined as a sequence of requests originating from the same client and the associated responses during a specific time period. Modern web applications utilize user sessions to facilitate the assignment of access or authorization rights, localization settings, etc.

Since HTTP is a stateless communication protocol, each requests only carry enough information for the server to act upon it. This means that session state can only reside on the client side.

For this reason, web applications utilizes cookies, URL parameters, URL arguments (on GET requests), body arguments (on POST requests), and other proprietary solutions for session tracking and management purposes.
## Session Identifier Security
