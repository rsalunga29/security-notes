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
## URL Authority Obfuscation
Starting from the URI structure, what we want to obfuscate is the Authority component of a URI:
```
    foo://example.com:8042/over/there?name=ferret#nose
    \_/   \______________/\_________/ \_________/ \__/
     |           |            |            |        |
   scheme     authority       path        query   fragment
```

Other than just the hostname and port, the Authority component can also be structured like the following:
```txt
[userinfo "@"] host [":" port]
```
### Obfuscating with userinfo
The `userinfo` subcomponent is used for authentication. If credentials are required to access a resource, they can be included here, and the login will be automatic. Otherwise, the subcomponent text is ignored by both the browser and the server. For example:
```txt
http://username:password@target-website.com:8042/admin
```

So, if we know that the resource does not require authentication, then we can use the following URI:
```txt
https://www.google.com@target-website.com/t/xss
```

`target-website.com` does not implement this kind of authentication, and will ignore the `www.google.com` part of the URI.
#### userinfo Unicode Support
Furthermore, the `userinfo` subcomponent supports Unicode.
```txt
https://✌(◕‿-)✌@hack.me
```
```txt
https://mail.google.com⁄mail⁄u⁄0⁄ʔpli=1#inbox@hack.me
```
#### Restrictions
However, now all browsers support this type of obfuscation technique. Firefox will throw error messages, while some versions of Opera and Google Chrome allows this behavior silently.
### Obfuscating with Host
