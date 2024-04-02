In PHP there are four different ways to specify a string literal:
- single quoted
- double quoted
- heredoc syntax
- nowdoc syntax

It is common to use single (`'`) or double (`"`) quoted delimiters when working with type string. The main difference is that, with single-quoted (`'`), variables and escape sequence for special characters are not expanded, but with double-quoted (`"`), they are.
## Single / Double Quoted Delimiters
```php
$expand = 'expand, nay they do';

// Variables do not $expand, \n\t also escapes except ' and \ at the end of the string \
echo 'Variables do not $expand, \n\t also escapes except \' and \ at the end of the string \\';

// Variables do not expand, nay they do,
//   also escapes
echo "Variables do not $expand, \n\t also escapes";
```
## Single / Double Quoted Escapes
The backslash (`\`) is used to escape strings in PHP.

The following table contains the list of escape sequences that PHP provides for special characters. Notice that it is possible to use octal and hexadecimal notations to represent characters.

| Sequence             | Meaning                                                                          |
| -------------------- | -------------------------------------------------------------------------------- |
| `\n`                 | linefeed (LF or `0x0A (10)` in ASCII)                                            |
| `\r`                 | carriage return (CR or `0x0D (13)` in ASCII)                                     |
| `\t`                 | horizontal tab (HT or `0x09 (9)` in ASCII)                                       |
| `\v`                 | vertical tab (VT or `0x0B (11)` in ASCII)                                        |
| `\f`                 | form feed (FF or `0x0C (12)` in ASCII)                                           |
| `\\`                 | backslash                                                                        |
| `\$`                 | dollar sign                                                                      |
| `\"`                 | double-quote                                                                     |
| `\[0-7]{1,3}`        | sequence of characters matching the regex is a character in octal notation       |
| `\x[0-9A-Fa-f]{1,2}` | sequence of characters matching the regex is a character in hexadecimal notation |
Example as follows:
```txt
//I Love Be3r
echo "I\x20L\x6fve\40B\145\63r";

\x20 is a space (hexadecimal)
\x6f is a latin small letter "O" (hexadecimal)
\40 is a space (octal)
\145 is a latin small letter "E" (octal)
\63 is a digit three (octal)
```
## Single / Double Quoted Variable Parsing
With the dollar sign (`$`), the parser tries to form a valid variable name. It is also possible to enclose the variable name in curly brackets (`{}`) to explicitly specify the end of the name.
```php
$s = "\x20"; //Space character

echo "I$sLove Beer"; //There's no $sLove variable > I Beer
echo "I{$s}Love Beer"; // > I Love Beer
echo "I${s}Love Beer"; // > I Love Beer
echo "I{${s}}Love Beer"; // > I Love Beer
```
Additionally, even array, object methods, and class functions with numerical obfuscation are allowed, as follows:
```php
$s = "\x20"; //Space character
$sp = " "; //Another space character

echo "I{$s[0]}Love{$sp[0]}Beer"; //> I Love Beer
echo "I{$s[(int)"I love Beer"]}Love{$sp[!true]}Beer";//> I Love Beer
echo ILoveBeer./**/.NULL; //> ILoveBeer
echo ILoveBeer.FALSE; //> ILoveBeer
echo "I{$s[eval($_GET['s'])]}Love Beer"; //Simple shell!> [SHELL-result]I Love Beer
```
## Heredoc and Nowdoc
PHP offers two alternatives to delimit strings: **Heredoc** and **Nowdoc**. The difference between the two is, Heredoc is for double-quoted strings while Nowdoc is for single-quoted strings.

Additionally, the identifier must contain only alphanumeric characters and underscores. It must also start with a non-digit character or underscore, as such, the following are valid:
```php
echo <<<⊶
It works!
⊶;
```
```php
echo <<<'🍺'
It works!
🍺;
```
```php
echo <<<✄
It works!
✄;
```
### Heredoc example
```php
$expand = 'expand, nay they do';
$hd = <<<HERE
Variables do not $expand, \n\t also escapes.\n This is
the Heredoc syntax. \n Notice there is no quotes around
the identifier (HERE)
HERE;
echo $hd;
```
The above code would output the following:
```txt
Variables do not expand, nay they do,
	also escapes.
This is the Heredoc syntax.
Notice there is no quotes around the identifier (HERE)
```
### Nowdoc example
```php
$expand = 'expand, nay they do';
$nd = <<<'NOW'
Variables do not $expand, \n\t also escapes.\n This is
the Nowdoc syntax. \n Notice the single quotes used to
enclose the identifier (NOW)
NOW;
echo $nd;
```
The above code would output the following:
```txt
Variables do not $expand, \n\t also escapes.\n This is
the Nowdoc syntax. \n Notice the single quotes used to
enclose the identifier (NOW)
```