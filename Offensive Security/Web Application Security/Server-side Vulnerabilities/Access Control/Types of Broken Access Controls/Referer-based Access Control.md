Some websites base access controls on the `Referer` header submitted in the HTTP request. The `Referer` header can be added to requests by browsers to indicate which page initiated a request.

For example, an application enforces access control over an admin page at `/admin`, but for sub-pages such as `/admin/deleteUser`, it only inspects the `Referer` header. If the `Referer` header contains the `/admin` URL, then the request is allowed.

In this case, the `Referer` header can be fully controlled by the attacker, by changing the value of the required `Referer` header, the attacker can forge direct requests to sensitive sub-pages and gain unauthorized access.