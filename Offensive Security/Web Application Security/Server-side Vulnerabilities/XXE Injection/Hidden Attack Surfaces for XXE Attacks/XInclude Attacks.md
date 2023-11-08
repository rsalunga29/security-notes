Some applications receive client-submitted data, converts it into an XML document and then parses the document. A typical example of this is when the client-submitted data is placed into a backend [SOAP](https://www.w3schools.com/xml/xml_soap.asp) request, which is then processed by the backend SOAP service.

This makes it impossible for an attacker to carry out a classic XXE attack, as it cannot define or modify the `DOCTYPE` element. However, an attacker might use `XInclude` instead which is a part of the XML specification that allows an XML document to be built from sub-documents.

An `XInclude` attack can be placed within any  data value in an XML document, which makes it possible to perform the attack even if you only control a single item of data within the document.

To perform an `XInclude` attack, an attacker need to reference the `XInclude` namespace and provide the path to the file that you wish to include:
```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude"> <xi:include parse="text" href="file:///etc/passwd"/></foo>
```
## Exploit Example
For example, imagine a shopping application that lets a user view whether an item is in stock in a particular store branch. To do this, the application sends an HTTP request.
```http
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

productId=1&storeId=1
```
The backend will embed the user input inside a server-side XML document that is then parsed. The attacker can modify the request with the following to exploit a `XInclud`