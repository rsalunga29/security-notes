"The ways of PHP obfuscation are infinite..."

Just like JavaScript, PHP is a dynamically typed language. PHP does not require/support explicit type definition in variable declaration. Basically, we can declare the same variable and as we assign different values (string, int, etc) the type of the variable changes. This is also called "type juggling".

For example, if we assign a string value to the variable `$joker`, it becomes a string, if you then assign an integer, the type changes, and so on.
```php
$joker = "1" // string(1) "1"
$joker++; // int(2)
$joker += 19.8; // float(21.8)
$joker = 8 + "7 -Ignore me please-"; // int(15)
$joker = "a string" + array("1.1 string")[0]; // float(1.1)
$joker .= ""; // string(1) "7"
$joker += ""; // int(7)
```
>Note: PHP versions 7 and above will throw warnings or even errors when executing type juggling.