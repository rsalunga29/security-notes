## Filter/WAF Detection
If we try the following payload (`?ip=127.0.0.1;id&&whoami`) and received any error message. It may indicate that we triggered a security mechanism, this might be because the web application has either detected a blacklisted character or a blacklisted command.

If the error message displayed a different page, with information like our IP and our request, this may indicate that it was denied by a WAF.
## Blacklisted Character and Commands
A web application may have a list of blacklisted characters, and if the command contains them, it would deny the request. A PHP code may look something like the following:
```php
$blacklist = ['&', '|', ';', 'whoami', 'id', ...SNIP...];
foreach ($blacklist as $malicious) {
	if (strpos($_POST['ip'], $malicious) !== false) {
		echo "Invalid input.";
	}
}
```
If any character or command in the string an attacker sent matches a value of the blacklist array, the request will be denied. However, in this example, the code is looking for an exact match of the provided character or command. An attacker can easily bypass this by using a different command or obfuscating their payload.
## Identifying Blacklisted Characters
## Identifying Blacklisted Commands (Linux)
