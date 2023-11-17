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
## Why is the same-origin policy necessary?
When a browser sends an HTTP request from one origin to another, any cookies, including authentication session cookies, relevant to the other domain are also sent as part of the request. This means that the response will be generated within the user's session, and include any relevant data that is specific to the user. Without the same-origin policy, if you visited a malicious website, it would be able to read your emails from Gmail, private messages from Facebook, etc.
## Same-origin Policy Implementation
The same-origin policy primarily controls JavaScript's access to cross-domain content or resources. For example, it allows embedding of images via the `<img>` tag, media via the `<video>` tag and JavaScript includes with the `<script>` tag. However, it restricts JavaScript on the page from reading the contents of these loaded cross-domain resources.

There are various exceptions to the same-origin policy:
- Some objects are writable but not readable cross-domain, such as the `location` object or the `location.href` property from iframes or new windows.
- Some objects are readable but not writable cross-domain, such as the `length` property of the `window` object (which stores the number of frames being used on the page) and the `closed` property.
- The `replace` function can generally be called cross-domain on the `location` object.
- You can call certain functions cross-domain. For example, you can call the functions `close`, `blur` and `focus` on a new window. The `postMessage` function can also be called on iframes and new windows in order to send messages from one domain to another.

<!-- @TODO: Link XSS from Client-side vulnerabilities -->
The same-origin policy is more relaxed when dealing with cookies, allowing access from all subdomains even though each subdomain is technically a different origin. This can be partially mitigated by using the `HttpOnly` cookie flag, it can also prevent using XSS from stealing cookies.

It is also possible to relax the same-origin policy using `document.domain`, so long as the specific domain is part of the FQDN (fully qualified domain name). For example, for `marketing.example.com` to read the contents of `example.com`, they both need to set `document.domain` to `example.com`. In the past, it was possible to set `document.domain` to a TLD such as `.com`, but modern browsers now prevent this.