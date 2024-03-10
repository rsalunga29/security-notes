Also known as SSRF, is a web security vulnerability that allows an attacker to abuse an application's functionality to perform internal and external requests to an unintended location, such as an attacker-controlled server or internal-only services within the target's infrastructure.

A successful SSRF attack can often result in:
- Interacting with known internal systems
- Discovering internal services via port scans
- Disclosing local/sensitive data
- Including files in the target application
- Leaking NetNTLM hashes using UNC Paths (Windows)
- Achieving remote code execution

SSRF attacks often exploit trust relationships to escalate an attack from the vulnerable application and perform unauthorized actions. These trust relationships might exist in relation to the server, or in relation to other back-end systems.

SSRF attacks are not limited to HTTP, you can use other protocols such as:
- `file://`
- `gopher://`
- `ssh://`

When hunting for SSRF vulnerabilities, we should consider looking for:
- Parts of HTTP requests, including URLs
- File imports such as HTML, PDFs, images, etc.
- Remote server connections to fetch data
- API specification imports
- Dashboards including ping and similar functionalities to check server statuses