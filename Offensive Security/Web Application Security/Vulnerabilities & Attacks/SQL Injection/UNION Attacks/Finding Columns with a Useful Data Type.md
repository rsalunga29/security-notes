Most data that you might want to retrieve is normally in string form. This means you need to find one or more columns in the original query whose data type is, or is compatible, with string data.

You can do this by submitting a series of `UNION SELECT` payloads that place a string value into each column in turn. For example:
```txt
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```
> Note: We can also do this without the `'` (i.e `target-website.com?id=3 UNION SELECT NULL,NULL,'a'-- -`)

If the column data type is not compatible with string data, the database will return an error:
```txt
Conversion failed when converting the varchar value 'a' to data type int.
```
However, if this error does not occur and the application's response contains some additional content including the injected string value, then the relevant column is suitable for retrieving string data.

Once successful, you can now proceed with the attack. Depending on the number of column that is string-value compatible, you can return the results in multiple column or in this example, a single column using string concatenation:
```txt
http://target-website.com?productId=1' UNION SELECT NULL,NULL,CONCAT('username','password') FROM users--
```