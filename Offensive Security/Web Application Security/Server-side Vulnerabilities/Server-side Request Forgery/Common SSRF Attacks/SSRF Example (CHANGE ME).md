In this example, we will be exploiting an internet-facing web application and work to get remote code execution on an internal host by chaining multiple SSRF vulnerabilities. The attack flow shall be as follows:
```
PENTESTER -> SSRF on Internet-facing App -> SSRF on Internal Web Server -> RCE on Local Web App.
```
First