Even if a cookie is set to `SameSite=Strict`, an attacker can still get around the limitation if they managed to find a gadget that results in a secondary requests within the same site.

<!-- @TODO: Link DOM-based open redirection on "client-side redirect" word -->
One possible gadget is a client-side redirect that dynamically constructs the redirect URL using attacker-controlled input like URL parameters.

This type of bypass works because, as far as browsers are concerned, these client-side redirects aren't really redirects at all. The resulting request is just treated as an ordinary, standalone request. Most importantly, it is a same-site request and includes all cookies related to the site, regardless of any restrictions in place.

*Note that the equivalent attack is not possible with server-side redirects. In this case, browsers recognize that the request to follow the redirect resulted from a cross-site request initially, so they still apply the appropriate cookie restrictions.*
## Example Exploit from PortSwigger Academy
1. Identify the `POST /my-account/change-email` request and notice that it is vulnerable to CSRF.
2. Look at the response of `POST /login` request and notice that