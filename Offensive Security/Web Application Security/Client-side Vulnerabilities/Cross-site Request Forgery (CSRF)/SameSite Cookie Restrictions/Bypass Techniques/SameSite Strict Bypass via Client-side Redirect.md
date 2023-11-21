Even if a cookie is set to `SameSite=Strict`, an attacker can still get around the limitation if they managed to find a gadget that results in a secondary requests within the same site.

<!-- @TODO: Link DOM-based open redirection on "client-side redirect" word -->
One possible gadget is a client-side redirect that dynamically constructs the redirect URL using attacker-controlled input like URL parameters.

This type of bypass works because, as far as browsers are concerned, these client-side redirects aren't really redirects at all. The resulting request is just treated as an ordinary, standalone request. Most importantly, it is a same-site request and includes all cookies related to the site, regardless of any restrictions in place.

*Note that the equivalent attack is not possible with server-side redirects. In this case, browsers recognize that the request to follow the redirect resulted from a cross-site request initially, so they still apply the appropriate cookie restrictions.*
## Example Exploit from PortSwigger Academy
1. Identify the `POST /my-account/change-email` request and notice that it is vulnerable to CSRF.
2. Look at the response of `POST /login` request and notice that the website explicitly specifies `SameSite=Strict` when setting session cookies.
3. Go to one of the blog posts and post an arbitrary comment. Observe tat you're initially sent to a confirmation page at `/post/comment/confirmation?postId=x` but after a few seconds, you're taken back to the blog post.
4. In the Burp Proxy history, notice that the redirect is handled client-side using the JavaScript file `/resources/js/commentConfirmationRedirect.js`.
5. Read through the code and notice that it dynamically constructs a client-side redirect URL by using the `postId` query parameter.
6. In the browser, visit the following URL and change the `postId` parameter into an arbitrary string `/post/comment/confirmation?postId=foo`. Notice that it redirects to a path containing the injected string `/post/foo`.
7. Inject a path traversal sequence to the `postId` parameter and observe it will redirect to the account page, `/post/comment/confirmation?postId=1/../../my-account`. This confirms we can use `postId` parameter to elicit a `GET` request for an arbitrary endpoint on the target site.
8. Use the following payload and execute a CSRF attack:
```html
<script>
	document.location = 'https://vulnerable-website.com/post/comment/confirmation?postId=1/../../my-account/change-email?email=pwned@normal-user.net&submit=1';
</script>
```