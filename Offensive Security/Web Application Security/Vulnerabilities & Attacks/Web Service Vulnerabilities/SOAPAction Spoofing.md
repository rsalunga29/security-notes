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

payload = ''

req = requests.post(
	'http://target-website.com/wsdl',
	data=payload,
	headers={"SOAPAction": '"ExecuteCommand"'}
)

print(req.content)
```
