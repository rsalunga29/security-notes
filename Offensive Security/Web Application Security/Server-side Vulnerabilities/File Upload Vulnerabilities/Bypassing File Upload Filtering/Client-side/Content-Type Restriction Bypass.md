Some applications uses the value of `Content-Type` HTTP header to determine the filetype of the file about to be uploaded. However, this doesn't work as an attacker can bypass this restriction by manipulating the HTTP request.

For example, an application allows a user to upload their own profile picture where it only accepts `image/jpeg` and `image/png` filetypes. An attacker can follow the following steps to force the application to accept a malicious file masquerading as either `image/jpeg` or `image/png`:
1. Using Burp Proxy, intercept the request. Observe that the `Content-Type` is set to `image/jpeg` and
![[content-type-bypass-2.png]]
2. aaa