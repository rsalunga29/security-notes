The first useful data type set in PHP obfuscation is related to numbers. With numerical data types, we can either access elements inside strings or inside arrays. Then, we can use them to generate characters and a great deal more.
## Access String / Integer Numbers
```php
$x = 'Giuseppe';

echo $x[0]; // decimal index (0) > 'G'
echo $x[0001]; // octal index (1) > 'i'
echo $x[0x02]; // hexadecimal index (2) > 'u'
echo $x[0b11]; // binary index (3) > 's'
```
The following image describes how the structure of integer literals are:
![[php-obfus-integer-literals.png]]
Thus, the following example is still valid code:
```php
$x='Giuseppe';
echo $x[0]; // decimal index (0) > 'G'
echo $x[00000000000001]; // octal index (1) > 'i'
echo $x[0x000000000002]; // hexadecimal index (2) > 'u'
echo $x[0b000000000011]; // binary index (3) > 's'
```
## Access String / Floating Numbers
Numerical data types also comprehend floating numbers. For example:
```php
$x='Giuseppe';

echo $x[0.1]; // floating (0.1) casted to 0 > 'G'
echo $x[.1e+1]; // exponential > 'i'
echo $x[0.2E+0000000000001]; // long exponential > 'u'
echo $x[1e+1-1E-1-5.999]; // exponential and floating expression (3.901) casted to 3 > 's'
```
The following image describes how the structure of floating point literals are:
![[php-obfus-float-literals.png]]
## Exotic Number Generation
The following is an example of an exotic number generation:
```php
$x='Giuseppe';

echo $x[FALSE]; // FALSE is 0 > 'G'
echo $x[TRUE]; // TRUE is 1 > 'i'
echo $x[count('hello')+true]; // count(object) is 1 > 'u'
echo $x["7rail"+"3er"-TRUE^0xA]; // PHP ignore trailing data
```

Additionally, it is also possible to use the type casting functionalities that PHP provides.
```php
$x='Giuseppe';

echo $x[(int)"a common string"]; // 0 > 'G'
echo $x[(int)!0]; // True (1) > 'i'
echo $x[(int)"2+1"]; // 2 > 'u'
echo $x[(float)"3.11"]; // 3 > 's'
echo $x[boolval(['.'])+(float)(int)array(0)+floatval('2.1+1.2=3.3')]; // True(1)+1+2.1 = 4.2 (float) > 'e'
```