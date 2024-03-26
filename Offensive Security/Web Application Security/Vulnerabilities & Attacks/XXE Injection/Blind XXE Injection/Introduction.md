Blind XXE vulnerabilities arise where the application is vulnerable to XXE Injection but does not return the values of any defined external entities within its response. This means that retrieval of server files is not possible, which makes blind XXE harder to exploit than regular XXE.

There are two ways to find and exploit blind XXE:
- Trigger an out-of-band network interactions, sometimes exfiltrating sensitive data within the interaction data.
- Trigger XML parsing errors in such a way the error message contains sensitive data.