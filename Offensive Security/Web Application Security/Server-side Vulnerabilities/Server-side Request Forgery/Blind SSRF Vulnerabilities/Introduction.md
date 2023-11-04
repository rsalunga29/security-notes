Blind SSRF occurs if you can cause the application to issue a backend HTTP request to a supplied URL, but doesn't return a response to the application's frontend.

This makes it harder to exploit as it cannot be trivially used to retrieve sensitive data but it could sometimes lead to a full remote code execution (RCE) on a server or other backend components.