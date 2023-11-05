File inclusion vulnerabilities allow an attacker to read sensitive files or sometimes execute files on a server. The vulnerability occurs due to the use of user-supplied input without proper validation.

This vulnerability is usually chained with [Path Traversal](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FPath%20Traversal%2FIntroduction) and [Server Side Request Forgery (SSRF)](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FServer-side%20Request%20Forgery%2FIntroduction), as this vulnerability requires one or the other to properly work.

There are two types of file inclusions:
1. Local File Inclusion - remot
2. Remote File Inclusion