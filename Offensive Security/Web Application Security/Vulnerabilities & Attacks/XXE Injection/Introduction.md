Also known as XML External Entity Injection is a vulnerability that allows an attacker to interfere with an application's processing of XML data. This vulnerability often happens when a poorly configured XML parser processes an XML input with a reference to an external entity.

This vulnerability often allows the attacker to view files on the server and interact with any backend or external systems that the application has access to.

XML external entities are a type of custom XML entity whose defined values are loaded from outside of the [DTD](https://portswigger.net/web-security/xxe/xml-entities) in which they are declared. External entities are particularly interesting from a security perspective because they allow an entity to be defined based on the contents of a file path or URL.

In some situations, an attacker can leverage a XXE vulnerability to escalate and perform [server-side request forgery (SSRF)](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FServer-side%20Request%20Forgery%2FIntroduction) attacks.
## How to Find XXE Vulnerabilities
The vast majority of XXE vulnerabilities can be found quickly and reliably using Burp Suite's [web vulnerability scanner](https://portswigger.net/burp/vulnerability-scanner).

Manually testing for XXE vulnerabilities generally involves:
- Testing for [file retrieval](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FXXE%20Injection%2FCommon%20XXE%20Attacks%2FExploiting%20XXE%20to%20Retrieve%20Files) by defining an external entity based on a well-known operating system file and using that entity in data that is returned in the application's response.
- Testing for [blind XXE vulnerabilities](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FXXE%20Injection%2FBlind%20XXE%20Injection%2FIntroduction) by defining an external entity based on a URL to a system that you control, and monitoring for interactions with that system. [Burp Collaborator](https://portswigger.net/burp/documentation/desktop/tools/collaborator) is perfect for this purpose.
> Note: If Burp Collaborator is not available, we can use [CanaryTokens](https://canarytokens.org/generate#) and [interactsh](https://github.com/projectdiscovery/interactsh) as alternatives.
- Testing for vulnerable inclusion of user-supplied non-XML data within a server-side XML document by using an [XInclude attack](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FServer-side%20Vulnerabilities%2FXXE%20Injection%2FHidden%20Attack%20Surfaces%20for%20XXE%20Attacks%2FXInclude%20Attacks) to try to retrieve a well-known operating system file.