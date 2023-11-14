While it is normal to inject malicious SQL payloads on query strings, you can still perform SQL injection attacks on any controllable input that is processed as a SQL query by the application. For example, some websites take input in JSON or XML format and uses it to query the database.

<!-- @TODO: Link Obfuscation from WAF Bypass -->
Using these different formats may provide ways to an attacker to obfuscate their payload that are blocked by web-application firewalls (WAF) or other defense mechanisms. For example, the following XML-based SQL Injection uses an XML escape sequence to encode the `S` character in `SELECT`:
```xml
<stockCheck>
    <productId>123</productId>
    <storeId>999 &#x53;ELECT * FROM information_schema.tables</storeId>
</stockCheck>
```