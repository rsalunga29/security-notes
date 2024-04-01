The first useful data type set in PHP obfuscation is related to numbers. With numerical data types, we can either access elements inside strings or inside arrays. Then, we can use them to generate characters and a great deal more.
## Access String / Integer Numbers
```php
$x = 'Giuseppe';

echo $x[0]; // decimal index (0) > 'G'
echo $x[0001]; // octal index (1) > 'i'
echo $x[0x02]; // hexadecimal index (2) > 'u'
echo $x[0b11]; // binary index (3) > 's'
```
