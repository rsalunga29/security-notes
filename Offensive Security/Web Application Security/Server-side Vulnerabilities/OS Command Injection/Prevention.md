The most effective way to prevent OS command injection is to never call out to OS command from application-layer code. A better alternative is to implement the require functionality using safer platform APIs.

In the event, that you have to call out OS commands with user-supplied input, then you need to implement effective validation such as:
- Validating against a whitelist of permitted values
- Validating that the input is the expected data type
- Validating that the input contains only alphanumeric characters, no other syntax or whitespace
- Never attempt to sanitize input by escaping shell metacharacters. In practice, this is just too error-prone and vulnerable to being bypassed by a skilled attacker.