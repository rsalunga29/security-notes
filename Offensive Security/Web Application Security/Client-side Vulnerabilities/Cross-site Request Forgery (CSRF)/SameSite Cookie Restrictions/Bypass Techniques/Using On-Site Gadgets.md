Even if a cookie is set to `SameSite=Strict`, an attacker can still get around the limitation if they managed to find a gadget that results in a secondary requests within the same site.

<!-- @TODO: Link DOM-based open redirection on "client-side redirect" word -->
One possible gadget is a client-side redirect that dynamically constructs the redirect URL using attacker-controlled input like URL parameters.

This type of bypass works because, as far as browsers are concerned, these client-side redirects aren't really redirects at all.