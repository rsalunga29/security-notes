## Session Hijacking
While it is challenging to prevent or remediate session hijacking, due to the fact that a valid session identifier grants access to an application by design. We can however, monitor or detect for any session hijacking attacks using session monitoring/anomaly detection solutions.
## Session Fixation
Session fixation can be remediated by generating a new session identifier upon an authenticated operation. Simply invalidating any pre-login session identifier and generating a new one post-login should be enough.

The following code snippets invalidates the current session and gets a new session.
### PHP
```php
session_regenerate_id(bool $delete_old_session = false): bool
```
### Java
```java
session.invalidate();
session = request.getSession(true);
```
### .NET
```asp
Session.Abandon();
```
> Note: `Session.Abandon()` is not sufficient for this task, as the session ID cookie is not removed from the user's browser. To address this, after `Session.Abandon()` is utilized, the cookie header must be overwritten or a more complex cookie-based session management must be implemented.
