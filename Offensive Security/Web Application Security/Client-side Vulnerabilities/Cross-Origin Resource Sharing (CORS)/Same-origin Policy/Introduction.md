The same-origin policy is a browser security mechanism that was defined to control access to data between web applications. For example, it aims to prevent a shopping application from accessing the response from your banking application during payment.

The following table shows how the same-origin policy will be applied if the `http://normal-website.com/example/example.html` tries to access other origins¹:

|URL accessed|Access permitted?|
|---|---|
|`http://normal-website.com/example/`|Yes: same scheme, domain, and port|
|`http://normal-website.com/example2/`|Yes: same scheme, domain, and port|
|`https://normal-website.com/example/`|No: different scheme and port|
|`http://en.normal-website.com/example/`|No: different domain|
|`http://www.normal-website.com/example/`|No: different domain|
|`http://normal-website.com:8080/example/`|No: different port²|
¹ An origin consists of the URI scheme, hostname, and port number
² Internet Explorer will allow this access because IE does not take account of the port number when applying the same-origin policy.
## Why is the same-origin policy necessary?
When a browser sends an HTTP request from one origin to another, any cookies, including authentication session cookies, relevant to the other domain are also sent as part of the request. This means that the response will be generated within the user's session, and include any relevant data that is specific to the user. Without the same-origin policy, if you visited a malicious website, it would be able to read your emails from Gmail, private messages from Facebook, etc.