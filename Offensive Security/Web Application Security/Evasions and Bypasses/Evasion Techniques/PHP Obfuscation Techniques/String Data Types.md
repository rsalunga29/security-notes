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
The back

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