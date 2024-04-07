DBMS "gadgets" can be used for construction of obfuscated payloads.
## Comments
Comments are useful to developers for clarifying SQL statements. However, it can also be used for commenting out a legitimate query and obfuscating portions of our payloads.
## Functions and Operators
Operators are constructs which behave generally like functions, but differs syntactically or semantically from usual functions. They can also be used as evasion techniques.

If we are dealing with numbers and comparisons, the most useful “gadgets” are the Arithmetic operators in conjunction with Bit Functions.
### Magic with Numbers
By manipulating the plus(+) and minus(-) characters we can generate a countless list of the number `1`:
```txt
http://target-website.com?id=1
http://target-website.com?id=--1
http://target-website.com?id=+-+-1
http://target-website.com?id=----2---1
```

We can also use Bitwise functions to generate the number `1` as follows:
```txt
http://target-website.com?id=1&1
http://target-website.com?id=0|1
http://target-website.com?id=13^12
http://target-website.com?id=8>>3
http://target-website.com?id=~-2
```

We can also use Logical Operators as follows:
```txt
http://target-website.com?id=NOT 0
http://target-website.com?id=!0
http://target-website.com?id=!1+1
http://target-website.com?id=
```