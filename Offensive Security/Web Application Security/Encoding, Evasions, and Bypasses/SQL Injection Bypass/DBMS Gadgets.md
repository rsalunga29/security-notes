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
In Oracle, the list shrinks back to what MySQL is using, plus the NULL char, like below:

| Codepoint | Character | Description |
| --------- | --------- | ----------- |
| 0         | U+0000    | NULL        |
### Non-Universal Characters
In all the DBMSs we can use the plus sign (`+`) to separate almost all the keywords except `FROM`. For example:
```sql
SELECT+name FROM employees WHERE+id=1 AND+name LIKE+'J%';
```
### Constants and Variables
For evasion purposes, knowing the SQL keywords is a must, as they can be useful during generation of strings, comparisons, etc.

[MySQL](https://dev.mysql.com/doc/refman/8.0/en/keywords.html), [MSSQL](https://learn.microsoft.com/en-us/sql/t-sql/language-elements/reserved-keywords-transact-sql?view=sql-server-ver16), and [Oracle](https://docs.oracle.com/cd/A97630_01/appdev.920/a42525/apb.htm) all have keywords which are reserved and require special treatment for use as identifiers.

The only way to obfuscate keywords is by manipulating upper/lower case variations like: `sELeCt`, `SEleCT`, etc...

Using `SHOW VARIABLES`, we can view the list of MySQL Server System Variables.

If we want to define a custom variable, then we need the
following notation:
```sql
SET @myvar={expression}
SET @myvar:={expression}
```
### Strings
In MySQL, we can define strings using single-quote (`'`) or double-quotes (`"`).

We can also define string laterals with the following character set: `_latin1'string'`. The character set that can be used has approximately 40 possible values and can use any of them preceded by an underscore character: `SELECT _ascii'Break Me'`

We can also use `N'literal'` or `n'literal'` to create a string in the National Character Set, for example:
```sql
SELECT N'mystring'
```

There is also `B'literal'` or `b'literal'` for defining Bit Literals, for example:
```sql
SELECT 'a'=B'1100001' # TRUE
```

Other literal notations are Hexadecimal:
```sql
SELECT X'4F485045'
SELECT 0x4F485045
```

MySQL also supports Unicode, below is a simple example of a Unicode select:
```sql
SELECT 'admin'='ąďṁĩň' #TRUE
```

In MSSQL, the literal is defined as either constant or scaler value, it can only be defined using single-quote (`'`). However, if the `QUOTED_IDENTIFIER` is enabled, we can use double-quotes (`"`).

In Oracle, literals are not allowed to use double-quote delimiters. Instead, the National Notation is used. For example:
```sql
SELECT N'Hello'...
SELECT nQ'("ąďṁĩň")'...
```

Escaping in SQL means using a backslash before both the single and double quotes. For example:
```sql
SELECT 'He\'llo'
SELECT 'He\%\_llo'
```
Furthermore, to escape quotes we can use the same character two times:
```sql
SELECT 'He''llo'
SELECT "He""llo"
```
If we try to escape a character that does not have a respective escaping sequence, the backslash will be ignored.

In MSSQL and Oracle, we can escape single-quotes by using two single-quotes:
```sql
SELECT 'He''llo'
```

For quoted strings, concatenation can be performed by placing the string next to each other:
```sql
SELECT 'he' 'll' 'o'
```

As an alternative, we can use functions like `CONCAT` and `CONCAT_WS`. For example:
```sql
SELECT CONCAT('He','ll','o')
SELECT CONCAT_WS(''. 'He', 'll', 'o')
```

It's also possible to concatenate using a mix of comments in C-style:
```sql
SELECT 'He'/**/'ll'/**/'o'
SELECT /**/'He'/**/'ll'/**/'o'/**/
SELECT /*!10000 'He' */'ll'/*****/'o'/*****/
```

In MSSQL, concatenation can be done using both the plus sign and `CONCAT` function. For example:
```sql
SELECT 'He'+'ll'+'o'
SELECT CONCAT('He','ll','o')
```

We can also obfuscate it using C-style comments:
```sql
SELECT 'He'/**/+/**/'ll'/**/+'o'
SELECT CONCAT(/**/'He',/**/1/**/,/**/'lo'/**/)
```

In Oracle, the operator is **||** and, from the function perspective, we can use **CONCAT** and **NVL**:
```sql
SELECT 'He'||'ll'||'o'
SELECT CONCAT('He','llo')
SELECT NVL('Hello', 'Goodbye')
```

We can also obfuscate it using C-style comments:
```sql
SELECT q'[]'||'He'||'ll'/**/'o'
SELECT CONCAT(/**/'He'/**/,/**/'ll'/**/)
```
### Integers
In MySQL, there is a special behavior when combining arithmetic operations with different types. For example:
```sql
SELECT ~'-2it\'s a kind of magic'
```

Numbers vs Booleans:
```sql
SELECT ... 1=TRUE
SELECT ... 2! =TRUE
SELECT ... OR 1
SELECT ... AND 1
```

Strings vs Numbers vs Booleans
```sql
SELECT ... VERSION()=5.5 #5.5.30
SELECT ... @@VERSION()=5.5 #5.5.30
SELECT ... ('type'+'cast')=0 #TRUE
SELECT ~'-2it\'s a kind of magic' #1
SELECT -'-1337a kind of magic'-25 #1337
```