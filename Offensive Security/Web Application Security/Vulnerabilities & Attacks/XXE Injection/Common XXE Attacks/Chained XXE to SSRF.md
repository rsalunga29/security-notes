Aside from retrieval of sensitive data, XXE attacks can be chained to perform SSRF. This is a serious vulnerability in which the server-side application can be forced to make HTTP request to any URL that the server can access.

To chain a XXE attack into a SSRF, an attacker needs to define an external XML entity using the target URL, and use the defined entity within a data value to return the response from the target URL. In this example, the external entity will cause the server to make a HTTP response to the internal system:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE haxxor [ <!ENTITY xxe SYSTEM "http://internal.target-website.com"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```