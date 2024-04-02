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
## Using String Output of Native PHP Objects
If we want to start from a string, we can use the Array native object as follows:
```php
$a = []; // Create an empty array object
$a = $a.!![]; // Convert the array to string > "Array"
$_ = $__ = ![]&!![]; // true & false generates the int(0) > 0
$__++; // Increment int(0) by one > 1
$_§ = $__§ = $a[$_]; // Access the position 0 of the "Array" string > "A"
$__§++; // Get the next char after A > "B"
echo $_§|$__§; // Echoes A|B > "C"
```