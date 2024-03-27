The Web Services Description Language also known as WSDL is an XML-based file exposed by web services that informs clients of the provided services/methods, including where they reside and the method-calling convention.

A web service's WSDL file should not always be accessible. Developers may not want to publicly expose a web service's WSDL file, or they may expose it through an uncommon location, following a security through obscurity approach. In the latter case, directory/parameter fuzzing may reveal the location and content of a WSDL file.

Once the WSDL file is found, it is recommended to fuzz for any parameters that may expose more information about the WSDL file.
> Note: WSDL files can be found in many forms, such as `/example.wsdl`, `?wsdl`, `/example.disco`, `?disco` etc. [DISCO](https://docs.microsoft.com/en-us/archive/msdn-magazine/2002/february/xml-files-publishing-and-discovering-web-services-with-disco-and-uddi) is a Microsoft technology for publishing and discovering Web Services.

