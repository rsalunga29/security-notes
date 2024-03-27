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
## Messages
Defines input and output operations that the web service supports. It describes the data being exchanged between the web service providers and the consumers.
```xml
<!-- Login Messages -->
<wsdl:message name="LoginSoapIn">
    <wsdl:part name="parameters" element="tns:LoginRequest"/>
</wsdl:message>
<wsdl:message name="LoginSoapOut">
    <wsdl:part name="parameters" element="tns:LoginResponse"/>
</wsdl:message>
<!-- ExecuteCommand Messages -->
<wsdl:message name="ExecuteCommandSoapIn">
    <wsdl:part name="parameters" element="tns:ExecuteCommandRequest"/>
</wsdl:message>
<wsdl:message name="ExecuteCommandSoapOut">
    <wsdl:part name="parameters" element="tns:ExecuteCommandResponse"/>
</wsdl:message>
```
## Operation
Defines the available SOAP actions alongside the encoding of each message.
```xml
<!-- Login Operaion | PORT -->
<wsdl:operation name="Login">
	<wsdl:input message="tns:LoginSoapIn"/>
	<wsdl:output message="tns:LoginSoapOut"/>
</wsdl:operation> 
```
## Port Type
Combines multiple message elements to form a complete one-way or round-trip operation. For example, it can combine one request and one response message into a single request/response operation, as shown above. A `portType` can define multiple operations.
```xml
<wsdl:portType name="HacktheBoxSoapPort">
    <!-- Login Operaion | PORT -->
    <wsdl:operation name="Login">
  	  <wsdl:input message="tns:LoginSoapIn"/>
  	  <wsdl:output message="tns:LoginSoapOut"/>
    </wsdl:operation>
    <!-- ExecuteCommand Operation | PORT -->
    <wsdl:operation name="ExecuteCommand">
  	  <wsdl:input message="tns:ExecuteCommandSoapIn"/>
  	  <wsdl:output message="tns:ExecuteCommandSoapOut"/>
    </wsdl:operation>
</wsdl:portType>
```
## Binding
Binds the operation into a particular port type. A client will call the relevant port type and, using the details provided by the binding, will be able to access the operations bound to this port type.
```xml
<wsdl:binding name="HacktheboxServiceSoapBinding" type="tns:HacktheBoxSoapPort">
    <soap:binding transport="http://schemas.xmlsoap.org/soap/http"/>
    <!-- SOAP ExecuteCommand Action -->
    <wsdl:operation name="ExecuteCommand">
  	  <soap:operation soapAction="ExecuteCommand" style="document"/>
  	  <wsdl:input>
  		  <soap:body use="literal"/>
  	  </wsdl:input>
  	  <wsdl:output>
  		  <soap:body use="literal"/>
  	  </wsdl:output>
    </wsdl:operation>
</wsdl:binding>
```
