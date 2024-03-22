In this [page](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FFile%20Inclusion%20Vulnerabilities%2FRead%20vs%20Execute), we see that some functions allows the inclusion of remote URLs, which lets attackers to include remote files, this is called Remote File Inclusion. This allows two main benefits:
1. Enumerating local-only ports and web applications (i.e. SSRF)
2. Gaining remote code execution by including a malicious script that we host
