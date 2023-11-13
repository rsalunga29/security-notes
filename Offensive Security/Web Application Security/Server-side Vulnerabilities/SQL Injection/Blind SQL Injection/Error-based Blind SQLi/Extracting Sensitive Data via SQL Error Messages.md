Verbose error messages are dangerous since it could include information that may be useful to an attacker. This is usually caused by misconfiguration of the database. For example, consider the following error message, which occurs after injecting a single quote into an `id` parameter:
```txt
Unterminated string literal started at position 52 in SQL SELECT * FROM tracking WHERE id = '''. Expected char
```
This shows the full query that the application has constructed using our input.