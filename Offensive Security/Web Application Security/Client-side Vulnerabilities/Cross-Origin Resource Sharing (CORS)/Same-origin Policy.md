The same-origin policy is a web browser security mechanism that was defined in response to potentially malicious cross-domain interactions, such as one website attacking another. It also restricts scripts on one origin from accessing data from another origin. An origin consists of a URI scheme, domain and port number. For example:
```txt
http://normal-website.com/example/example.html
```

The following table shows how the same-origin policy will be applied if the URL above tries to access other origins:

|URL accessed|Access permitted?|
|---|---|
|`http://normal-website.com/example/`|Yes: same scheme, domain, and port|
|`http://normal-website.com/example2/`|Yes: same scheme, domain, and port|
|`https://normal-website.com/example/`|No: different scheme and port|
|`http://en.normal-website.com/example/`|No: different domain|
|`http://www.normal-website.com/example/`|No: different domain|
|`http://normal-website.com:8080/example/`|No: different port¹|
¹ Internet Explorer will allow this access because IE does not take account of the port number when applying the same-origin policy.

Due to how browser works when sending HTTP request from one origin to another, any cookies including authenticatio