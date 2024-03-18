The HTTP response codes 30x are used for redirections.
## Permanent redirections
These redirections are meant to last forever. They imply that the original URL should no longer be used, and replaced with the new one. During permanent redirections, you should see the following HTTP codes in the response:
- 301 Moved Permanently
- 308 Permanent Redirect
## Temporary redirections
Sometimes the requested resource can't be accessed from its canonical location, but it can be accessed from another place. In this case, a temporary redirect can be used. During temporary redirections, you should see the following HTTP codes in the response:
- 302 Found
- 303 See Other
- 307 Temporary Redirect
## Bypass
Before doing any bypass, we must first check the HTTP redirect response in a proxy tool such as Burp, there will be cases where the redirects are being done on the client-side, 