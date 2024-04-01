URIs are fundamental elements of Internet communications. They provide a Uniform (local and remote), Resource Identifier
and are central in the web navigation system.

Sometimes, to exploit a vulnerability, one may require a degree of social engineering, making URI obfuscation very useful. Additionally, it can bypass some filtering systems but also shorten the payload to respect a length limit.
## URL Shortening
URL shortening is a technique in which a URL may be shorter in length and still direct to the required page. We can use [bit.ly](https://bitly.com/) or [yourls](https://yourls.org/) for this purpose.

Basically, an HTTP Redirect (301 Moved Permanently) header is sent from the domain name that is short to the web page that has a long URL.

However, due to prevalent use as an attack vector, most service providers have implemented a feature in order to preview where the shortened URL points to.
## URL Hostname Obfuscation
Almost everyone are used to viewing URL in formats like `https://target-website.com/s/#n:xss`.

But, according to RFC 3986, the following are also valid URLs:
- `https://target-website.com:443`
- `https://_[this_is_valid_]_@target-website.com`

What we want to obfuscate here is the Authority component of a URI:
```
         foo://example.com:8042/over/there?name=ferret#nose
         \_/   \______________/\_________/ \_________/ \__/
          |           |            |            |        |
       scheme     authority       path        query   fragment
```

which is structured as follows:
```txt
[userinfo "@"] host [":" port]
```