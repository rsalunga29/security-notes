As described by W3C:
> _"Web services provide a standard means of interoperating between different software applications, running on a variety of platforms and/or frameworks. Web services are characterized by their great interoperability and extensibility, as well as their machine-processable descriptions thanks to the use of XML."_

In short, web services enable applications to communicate with each other.

There are multiple approaches/technologies for providing and consuming web services:
## XML-RPC
[XML-RPC](http://xmlrpc.com/spec.md) uses XML for encoding/decoding the remote procedure call (RPC) and the respective parameter(s). HTTP is usually the transport of choice.
### Request
```http
POST /RPC2 HTTP/1.0
User-Agent: Frontier/5.1.2 (WinNT)
Host: betty.userland.com
Content-Type: text/xml
Content-length: 181

<?xml version="1.0"?>
<methodCall>
	<methodName>examples.getStateName</methodName>
	<params>
	    <param>
	 		<value><i4>41</i4></value>
 		</param>
	</params>
</methodCall>
```
### Response
```http
HTTP/1.1 200 OK
Connection: close
Content-Length: 158
Content-Type: text/xml
Date: Fri, 17 Jul 1998 19:55:08 GMT
Server: UserLand Frontier/5.1.2-WinNT

<?xml version="1.0"?>
<methodResponse>
    <params>
    <param>
	<value><string>South Dakota</string></value>
	</param>
  	</params>
</methodResponse>
```
## JSON-RPC
## SOAP (Simple Object Access Protocol)
Lorem Ipsum

Additionally, there are other slightly different SOAP envelopes
#### WS-BPEL
#### RESTful