A token should expire after the user has been inactive for a given amount of time, for example, after 1 hour, and should expire even if there is activity after a given amount of time, such as 24 hours. Additionally, if the user gets more grants during a sudo-like session, the token must change. If a token never expires or changes, it might be prone to a session fixation attack.

Session fixation is an attack carried out by tricking or phishing a user to use a link that has a predefined session ID that is unknown to the application. When the user logs in to the vulnerable web application using the predefined session ID, the attacker can now proceed to a [Session Hijacking attack](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FSession%20Security%2FSession%20Hijacking).

Session Fixation attacks are usually mounted in three stages:
#### Stage 1: Attacker manages to obtain a valid session identifier
Authenticating to an application is not the only way to get a valid session ID, a large number of applications assign valid session IDs to anyone who visits them. However, an attacker can still create an account on the target application and obtain a valid session identifier.

#### Stage 2: Attacker manages to fixate a valid session identifier
The scenario on stage 1 is expected behavior, but it can turn into a session fixation vulnerability if:
- The assigned session ID pre-login remains the same post-login
- Session IDs are being accepted from URL query strings or POST data and being passed to the application.

If, for example, a session-related parameter is included in the URL (and not on the cookie header) and any specified value eventually becomes a session identifier, then the attacker can fixate a session. For example,
#### Stage 3: Attacker tricks the victim into establishing a session using the abovementioned session identifier
All the attacker has to do is craft a URL and lure the victim into visiting it. If the victim does so, the web application will then assign this session identifier to the victim.

The attacker can then proceed to a session hijacking attack since the session identifier is already known.