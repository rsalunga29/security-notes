DBMS "gadgets" can be used for construction of obfuscated payloads.
## Comments
Comments are useful to developers for clarifying SQL statements. However, it can also be used for commenting out a legitimate query and obfuscating portions of our payloads.
## Functions and Operators
Operators are constructs which behave generally like functions, but differs syntactically or semantically from usual functions. They can also be used as evasion techniques.

If we are dealing with numbers and comparisons, the most useful “gadgets” are the Arithmetic operators in conjunction with Bit Functions.
### Magic with Numbers
By manipulating the plus(+) and minus(-) characters we can generate a countless list of the number `1`:
```txt
...?id=1
...?id=--1
...?id=+-+-1
...?id=----2---1
```

We can also use Bitwise functions to generate the number `1` as follows:
```txt
...?id=1&1
...?id=0|1
...?id=13^12
...?id=8>>3
...?id=~-2
```

We can also use Logical Operators as follows:
```txt
...?id=NOT 0
...?id=!0
...?id=!1+1
...?id=1&&1
...?id=1 || NULL
...?id=1 XOR 1
```

A number can also be generated using Regular Expression Operators to match a string and get `0` or `1`, like the following:
```txt
...?id={anything} REGEXP '.*'
...?id={anything} NOT REGEXP '{randomkeys}'
...?id={anything} RLIKE '.*'
...?id={anything} NOT RLIKE '{randomkeys}'
```

Comparison Operators are useful for generating numbers as well:
```txt
...?id=GREATEST(0,1)
...?id=COALESE(NULL,1)
...?id=ISNULL(1/0)
...?id=LEAST(2,1)
```

Oracle is must more restrictive. To use arithmetic operators, we must created a valid expression to avoid errors:
```txt
...?id=1
...?id=--1 < this doesnt work
...?id=+-+-1 < this doesnt work
...?id=-(-1)
...?id=-(1)*-(1)
```

In Oracle, to combine values, functions and operators into expressions, we must follow the list of Conditions mixed to Expression:
```sql
SELECT name FROM employees WHERE id=some(1)
```
### Intermediary Characters
Blank spaces are useful in separating functions, operators, declarations, and so forth, basically intermediary characters. However, there is non-common characters that can be used. For example:
```sql
SELECT[CHAR]name[CHAR]FROM[CHAR]employees;
```

In MySQL, the "UNIVERSAL" characters allowed as whitespaces are:

| Codepoint | Character | Description          |
| --------- | --------- | -------------------- |
| 9         | U+0009    | character tabulation |
| 10        | U+000A    | Life feed (LF)       |
| 11        | U+000B    | Line Tabulation      |
| 12        | U+000C    | Form feed            |
| 13        | U+000D    | Carriage return (CR) |
| 32        | U+0020    | Space                |
In MSSQL, the list of Universal characters allowed as a whitespace are large. Essentially, all the ASCII Control Characters, the space and the no-break space are allowed.

| Codepoint | Character | Description    |
| --------- | --------- | -------------- |
| 160       | U+00A0    | No-break space |
In Oracle