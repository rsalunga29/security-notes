Like in [JavaScript](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FEvasions%20and%20Bypasses%2FEvasion%20Techniques%2FJavaScript%20Obfuscation%20Techniques%2FNon-alphanumeric%20JS%20Encoding), in PHP it is also possible to write non-alphanumeric encoded code. The mechanism is similar but not the same.

This was first discovered by Gareth Hayes in a blog posts: [Non alphanumeric code in PHP](http://www.thespanner.co.uk/2011/09/22/non-alphanumeric-code-in-php/)  and [PHP nonalpha tutorial](http://www.thespanner.co.uk/2012/08/21/php-nonalpha-tutorial/).
## Arithmetic Operators
PHP follows Perl's convention when dealing with arithmetic operations on character vairables. For example:
```php
$§ = 'a';
$§++; //$§ = 'b'
$§ = 'z';
$§++; //$§ = 'aa'
$§ = 'A';
$§++; //$§ = 'B'
$§ = 'a1';
$§++; //$§ = 'a2'
```
Furthermore, character variables can only be incremented and not decremented. Only plain ASCII alphabets and digits are supported:
```php
$§ = 'a';
$§--; //$§ = 'a'
$§ = 'è';
$§++; //$§ = 'è'
```
## Bitwise Operators
It is also possible to use bitwise operators on strings:
```php
echo A&B; //> @
echo A|B; //> C
echo A^B; //U+0003 END OF TEXT
echo ~A; //U+00BE VULGAR FRACTION THREE QUARTERS> 3⁄4
echo A<<B; //> 0
```