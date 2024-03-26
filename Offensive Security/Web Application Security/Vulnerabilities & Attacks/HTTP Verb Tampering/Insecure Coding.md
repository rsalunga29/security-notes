Insecure coding practices also causes HTTP Verb Tampering vulnerabilities, this vulnerability is much more common as it is due to mistakes made by developers while coding.

This vulnerability typically occurs when a developer applies specific filters or patches to mitigate particular vulnerabilities or issues while not covering all HTTP methods with that filter/patch. For example, a web page is vulnerable to SQL injection and the developer mitigated this vulnerability by applying the following patch:
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

Another example is the following PHP code:
```php
if (isset($_REQUEST['filename'])) {
    if (!preg_match('/[^A-Za-z0-9. _-]/', $_POST['filename'])) {
        system("touch " . $_REQUEST['filename']);
    } else {
        echo "Malicious Request Denied!";
    }
}
```
If we were only considering Command Injection vulnerabilities, we would say that this is securely coded. The `preg_match` function properly looks for unwanted characters and does not allow the input to go into the command if any special characters are found. However, the vulnerability is not due to command injections due to to the inconsistent use of HTTP methods.

We see that the `preg_match` filter only checks for special characters in `POST` parameters with `$_POST['filename']`. However, the final `system` command uses the `$_REQUEST['filename']` variable, which covers both `GET` and `POST` parameters. This means, if an attacker uses `GET` request to send the malicious command which include special characters, the security filter will be bypassed as the `GET` method is not being checked for them.