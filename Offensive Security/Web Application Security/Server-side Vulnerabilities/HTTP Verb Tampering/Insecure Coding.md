Insecure coding practices causes HTTP Verb Tampering vulnerabilities, this vulnerability is much more common as it is due to mistakes made by developers while coding 


This typically occurs when a developer applies specific filters or patches to mitigate particular vulnerabilities or issues while not covering all HTTP methods with that filter/patch. For example, a web page is vulnerable to SQL injection and the developer mitigated this vulnerability by applying the following patch:
```php
...[TRIM]...
$pattern = "/^[A-Za-z\s]+$/";

if(preg_match($pattern, $_GET["code"])) {
    $query = "Select * from ports where port_code like '%" . $_REQUEST["code"] . "%'";
    ...SNIP...
}
```
As the sanitization filter is being only applied on the `GET` parameter, if the `GET` request don't contain any malicious characters, then the query would execute. However, when the query is executed the `$_REQUEST["code"]` parameter is being used, which may contain `POST` parameters, leading to an inconsistency in the use of HTTP verbs.

Additionally, if an attacker uses `POST` request to perform the SQL injection, in which case the `GET` parameters if empty, the request would still pass the security filter which would make the function still vulnerable to SQL injection.