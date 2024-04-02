PHP has another interesting feature that is useful for obfuscation, that is called **Variable Variables**.

The notation is simple and is as follows:
- `$var` > variable name.
- `$$var` > variable of `$var` variable.

Another example:
```php
$x = 'Love'; //Variable
$$x = 'Beer'; //Variable variable (now becomes $Love)

echo $x; //> Love
echo $$x; //> Beer
echo $Love; //> Beer
echo ${Love}; //> Beer
echo ${"Love"}; //> Beer

echo "$x ${$x}"; //> Love Beer
echo "$x ${Love}"; //> Love Beer
```

Furthermore, it is also possible to add more dollar signs, making it very easy to create a code that is very hard to read. For example, in the code below, we will be using chained dollar signs:
```
$x = "I";
$I = "Love";
$Love = "Beer";
$Beer = "So";
$So = "Much";

echo $x; //>I
echo $$x; //>Love
echo $$$x; //>Beer
echo $$$$x; //>So
echo $$$$$x; //>Much
echo $x.$$x.$$$x.$$$$x.$$$$$x; //>ILoveBeerSoMuch
```

Using the same technique - chained dollar signs, we can access the `$_SERVER` superglobal as follows:
```php
$$$$$$$$$$s = '_SERVER';

var_dump($$$$$$$$$$s); //> NULL
var_dump($$$$$$$$$$$s); //> string(7) "_SERVER"
var_dump($$$$$$$$$$$$s); //> the $_SERVER array
```