The [WSDL version 1.1](https://www.w3.org/TR/2001/NOTE-wsdl-20010315) layout consists of the following elements.
## Definition
The root element of all WSDL files. Inside the definition, the name of the web service is specified, all namespaces used across the WSDL document are declared, and all other service elements are defined.
```xml
<wsdl:definitions targetNamespace="http://tempuri.org/" 

    <wsdl:types></wsdl:types>
    <wsdl:message name="LoginSoapIn"></wsdl:message>
    <wsdl:portType name="HacktheBoxSoapPort">
  	  <wsdl:operation name="Login"></wsdl:operation>
    </wsdl:portType>
    <wsdl:binding name="HacktheboxServiceSoapBinding" type="tns:HacktheBoxSoapPort">
  	  <wsdl:operation name="Login">
  		  <soap:operation soapAction="Login" style="document"/>
  		  <wsdl:input></wsdl:input>
  		  <wsdl:output></wsdl:output>
  	  </wsdl:operation>
    </wsdl:binding>
    <wsdl:service name="HacktheboxService"></wsdl:service>
</wsdl:definitions>
```
## Data Types
The data types to be used in the exchanged messages.
```xml
<wsdl:types>
    <s:schema elementFormDefault="qualified" targetNamespace="http://tempuri.org/">
  	  <s:element name="LoginRequest">
  		  <s:complexType>
  			  <s:sequence>
  				  <s:element minOccurs="1" maxOccurs="1" name="username" type="s:string"/>
  				  <s:element minOccurs="1" maxOccurs="1" name="password" type="s:string"/>
  			  </s:sequence>
  		  </s:complexType>
  	  </s:element>
  	  <s:element name="LoginResponse">
  		  <s:complexType>
  			  <s:sequence>
  				  <s:element minOccurs="1" maxOccurs="unbounded" name="result" type="s:string"/>
  			  </s:sequence>
  		  </s:complexType>
  	  </s:element>
  	  ...[SNIP]...
    </s:schema>
</wsdl:types>
```