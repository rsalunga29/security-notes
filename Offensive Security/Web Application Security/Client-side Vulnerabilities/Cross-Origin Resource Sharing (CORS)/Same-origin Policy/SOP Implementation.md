The same-origin policy primarily controls JavaScript's access to cross-domain content or resources. For example, it allows embedding of images via the `<img>` tag, media via the `<video>` tag and JavaScript includes with the `<script>` tag. However, it restricts JavaScript on the page from reading the contents of these loaded cross-domain resources.

There are various exceptions to the same-origin policy:
- Some objects are writable but not readable cross-domain, such as the `location` object or the `location.href` property from iframes or new windows.
- Some objects are readable but not writable cross-domain, such as the `length` property of the `window` object (which stores the number of frames being used on the page) and the `closed` property.
- The `replace` function can generally be called cross-domain on the `location` object.
- You can call certain functions cross-domain. For example, you can call the functions `close`, `blur` and `focus` on a new window. The `postMessage` function can also be called on iframes and new windows in order to send messages from one domain to another.

The same-origin policy is more relaxed when dealing with cookies, allowing access from all subdomains even though each subdomain is technically a different origin. This can be partially mitigated by using the `HttpOnly` cookie flag, which can also prevent using [XSS](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Site%20Scripting%2FIntroduction) for stealing cookies.

It is also possible to relax the same-origin policy using `document.domain`, so long as the specific domain is part of the FQDN (fully qualified domain name). For example, for `marketing.example.com` to read the contents of `example.com`, they both need to set `document.domain` to `example.com`. In the past, it was possible to set `document.domain` to a TLD such as `.com`, but modern browsers now prevent this.