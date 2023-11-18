Verbose error messages are dangerous since it could include information that may be useful to an attacker. This is usually caused by misconfiguration of the database. For example, consider the following error message, which occurs after injecting a single quote into an `id` parameter:
```txt
Unterminated string literal started at position 52 in SQL SELECT * FROM tracking WHERE id = '''. Expected char
```
This shows the full query that the application has constructed including our injected input, which makes it easier for us to construct a valid query containing a malicious payload.

Occasionally, you can even induce the application to generate an error message that contains some of the data that is returned by the query, turning a blind SQL injection into a visible one. You can do this by using the `CAST()` function, which enables you to convert one data type to another. For example:
```txt
productId=1' AND CAST((SELECT example_column FROM example_data) AS int)--
```
Often, the data that you're string to read is a string. Attempting to convert it to an incompatible data type, such as `int`, may cause the application to return an error:
```txt
ERROR: invalid input syntax for type integer: "Example data"
```
## Example from PortSwigger Academy
[![ Portswigger Web Academy - Visible Error-based SQL Injection - Lab Walkthrough ](https://img.youtube.com/vi/efs1fS02--U/0.jpg)](https://www.youtube.com/watch?v=efs1fS02--U)