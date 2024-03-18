## HTTP Verbs/Methods Fuzzing
Try using different verbs/methods to access the page then enumerate the value of response headers, maybe some additional information may be given. For example, a `200 OK` response to `HEAD` verb with `Content-Length: 55` means that the `HEAD` verb can access the info.

We can also use the `X-HTTP-Method-Override` header to overwrite the verb that is being used.

Additionally, when using `TRACE` verb, there are chances where we can also see the headers added by intermediate proxies in the response.
## HTTP Headers Fuzzing
