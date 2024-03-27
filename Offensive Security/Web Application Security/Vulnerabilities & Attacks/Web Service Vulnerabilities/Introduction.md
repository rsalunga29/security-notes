As described by W3C:
> _"Web services provide a standard means of interoperating between different software applications, running on a variety of platforms and/or frameworks. Web services are characterized by their great interoperability and extensibility, as well as their machine-processable descriptions thanks to the use of XML."_

In short, web services enable applications to communicate with each other.

There are multiple approaches/technologies for providing and consuming web services:
## XML-RPC
[XML-RPC](http://xmlrpc.com/spec.md) uses XML for encoding/decoding the remote procedure call (RPC) and the respective parameter(s). HTTP is usually the transport of choice.

**Example HTTP Request**
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

**Example HTTP Response**
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
[JSON-RPC](https://www.jsonrpc.org/specification) uses JSON to invoke functionality. HTTP is usually the transport of choice.

**Example HTTP Request**
```http
POST /ENDPOINT HTTP/1.1
Host: ...
Content-Type: application/json-rpc
Content-Length: ...

{"method": "sum", "params": {"a":3, "b":4}, "id":0}
```

**Example HTTP Response**
```http
HTTP/1.1 200 OK
...
Content-Type: application/json-rpc

{"result": 7, "error": null, "id": 0}
```
## SOAP (Simple Object Access Protocol)
SOAP also uses XML but provides more functionalities than XML-RPC. SOAP defines both a header structure and a payload structure. The former identifies the actions that SOAP nodes are expected to take on the message, while the latter deals with the carried information.

Anatomy of a SOAP Message
- `soap:Envelope`: (Required block) Tag to differentiate SOAP from normal XML. This tag requires a `namespace` attribute.
- `soap:Header`: (Optional block) Enables SOAP’s extensibility through SOAP modules.
- `soap:Body`: (Required block) Contains the procedure, parameters, and data.
- `soap:Fault`: (Optional block) Used within `soap:Body` for error messages upon a failed API call.

**Example HTTP Request**
```http
POST /Quotation HTTP/1.0
Host: www.xyz.org
Content-Type: text/xml; charset = utf-8
Content-Length: nnn

<?xml version = "1.0"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV = "http://www.w3.org/2001/12/soap-envelope" SOAP-ENV:encodingStyle = "http://www.w3.org/2001/12/soap-encoding">
	<SOAP-ENV:Body xmlns:m = "http://www.xyz.org/quotations">
		<m:GetQuotation>
			<m:QuotationsName>MiscroSoft</m:QuotationsName>
		</m:GetQuotation>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

**Example HTTP Response**
```http
HTTP/1.0 200 OK
Content-Type: text/xml; charset = utf-8
Content-Length: nnn

<?xml version = "1.0"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV = "http://www.w3.org/2001/12/soap-envelope" SOAP-ENV:encodingStyle = "http://www.w3.org/2001/12/soap-encoding">
	<SOAP-ENV:Body xmlns:m = "http://www.xyz.org/quotation">
		<m:GetQuotationResponse>
			<m:Quotation>Here is the quotation</m:Quotation>
		</m:GetQuotationResponse>
	</SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

Additionally, there are other slightly different SOAP envelopes:
**WS-BPEL**
- WS-BPEL web services are essentially SOAP web services with more functionality for describing and invoking business processes.
- WS-BPEL web services heavily resemble SOAP services. For this reason, they will not be included in this module's scope.

**RESTful**
REST web services usually use XML or JSON. WSDL declarations are supported but uncommon. HTTP is the transport of choice, and HTTP verbs are used to access/change/delete resources and use data.