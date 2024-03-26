File upload vulnerabilities arises when a web server allows users to upload files into its filesystem without validating things like the name, filetype, contents, or size. Failing to enforce restrictions could mean that even a basic image upload function can be used to upload arbitrary and potentially dangerous files instead.

For example, failing to validate file types can allow an attacker to upload certain file types (such as `.php` and `.jsp`) which are web shells that enable remote code execution (RCE) resulting in an attacker taking full control of the server.

In some cases, the act of uploading a file in itself is enough to cause damage, as it can allow an attacker to overwrite critical server files simply by uploading a file with the same name. If the server is vulnerable to [directory traversal](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FPath%20Traversal%2FIntroduction), attackers can also even upload files to unexpected locations. This is caused by failure to validate the filename.

Finally, failing to make sure that the size of the file falls within an expected thresholds could fill available disk space, resulting in a denial-of-service (DoS) attack.
## Identifying Allowed File Types
One easy method to determine what language runs the web application is to visit the `/index.ext` page, where we would swap out `ext` with various common web extensions, like `php`, `asp`, `aspx`, among others, to see whether any of them exist.

We do not need to do this manually, of course, as we can use a tool like Burp Intruder for fuzzing the file extension using a Web Extensions wordlist.

Several other techniques may help identify the technologies running the web application, like using the Wappalyzer extension, which is available for all major browsers. Once added to our browser, we can click its icon to view all technologies running the web application.