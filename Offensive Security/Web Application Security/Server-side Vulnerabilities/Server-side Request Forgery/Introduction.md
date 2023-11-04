Also known as SSRF, is a web security vulnerability that allows an attacker to cause the server-side application to make request to an unintended location such as an attacker-controlled server or internal-only services within the target's infrastructure.

A successful SSRF attack can often result in unauthorized actions or access to sensitive data. In worst cases, an SSRF can lead to an attacker performing arbitrary command execution.

SSRF attacks often exploit trust relationships to escalate an attack from the vulnerable application and perform unauthorized actions. These trust relationships might exist in relation to the server, or in relation to other back-end systems.

SSRF attacks are not limited to HTTP, you can use other protocols such as:
- `file://`
- `gopher://`
- `ssh://`