A "fat GET" request is a `GET` request that includes a request body. By sending this type of `GET` request, an attacker can force the caching system to cache a response that contains an attacker-controlled value. 


it is possible to force the caching system to cache a response that contains user-controlled input. This cached response can be later served to a victim resulting in various vulnerabilities.

If the request body is unkeyed and included in the response, it can create an opportunity for cache poisoning.

By sending a `GET` request with a request body containing malicious payload, the response will be cached. Unsuspecting users who are then sending a regular `GET` request that matches the same cache key, will receive the poisoned request.

In some cases, it may also be possible to use the `X-HTTP-Method-Override` header to trick the application into treating a fat `GET` request as a normal `POST` request.