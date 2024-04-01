JavaScript is a loosely typed language, meaning you don't have to specify what type of information will be stored in a variable in advance. This behaviors helps in obfuscating JavaScript codes.

For example, you can cast a variable to String as follows:
```js
//returns "1234"
"" + 1234
1234 + ""

//returns "1234"
[] + 1234
1234 + []

x = "hello"
[1,"a",x] //returns [1, "a", "hello"]
[1,"a",x]+"" //returns "1,a,hello"
```
## Non-alphanumeric JavaScript Encoding
Among the many ways of encoding JavaScript, there is an interesting technique you should know called Non-alphanumeric JavaScript Encoding.
> Note: Read more about non-alphanumeric JS [here](https://portswigger.net/research/executing-non-alphanumeric-javascript-without-parenthesis).

This technique first appeared on the sla.ckers forum in late 2009 by Yosuke Hasegawa. Basically, Hasegawa showed a way to encode JS code by using non-alphanumeric characters. For example:
```js
_=[]|[];$=_++;__=(_<<_);___=(_<<_)+_;____=__+__;_____=__+___;$$=({}+"")[_____]+  
({}+"")[_]+({}[$]+"")[_]+(($!=$)+"")[___]+(($==$)+"")[$]+(($==$)+"")[_]+(($==$)  
+"")[__]+({}+"")[_____]+(($==$)+"")[$]+({}+"")[_]+(($==$)+"")[_];$$$=(($!=$)+""  
)[_]+(($!=$)+"")[__]+(($==$)+"")[___]+(($==$)+"")[_]+(($==$)+"")[$];$_$=({}+"")  
[_____]+({}+"")[_]+({}+"")[_]+(($!=$)+"")[__]+({}+"")[__+_____]+({}+"")[_____]+  
({}+"")[_]+({}[$]+"")[__]+(($==$)+"")[___]; ($)[$$][$$]($$$+"('"+$_$+"')")();
```

The above code would execute an `alert('cool code')`. This "magic" is strongly related to the loosely typed nature of JavaScript!
### Boolean
There are many ways to return a Boolean value using non-alphanumeric characters. For example:

**True**
- `!![]`
- `!!{}`
- `!""`
- `[]==""`

**False**
- `![]`
- `!{}`
- `!!""`
- `[]=={}`

We can also extract the Boolean values in string form by combining non-alphanumeric characters. For example:
- `[!![]]+""` returns "true".
- `[![]]+""` returns "false".
### Numbers
Numbers can also be created, for example `0` can be created as follows:
- `+""` or `+[]`
- `-""` or `-[]`
- `-+-+""` or `-+-+[]`
- `![]+![]`
- `![]+!{}`
- `![]+!!""`

Additional example below, remember `TRUE` is `1` and `FALSE` is `0`. Therefore, to generate a number `1`, we can do `TRUE+FALSE` and `2` is `TRUE+TRUE`.

| Number | Non-alphanumeric Representation                                  |
| ------ | ---------------------------------------------------------------- |
| 0      | `+[]` or `+""` or `![]+!{}`                                      |
| 1      | `+!![]` or `![]+!""` or `![]+!![]` or `~[]*~[]` or `++[[]][+[]]` |
| 2      | `!![]+!![]` or `++[++[[]][+[]]][+[]]`                            |
| 3      | `!![]+!![]+!![]`                                                 |
| 4      | `!![]+!![]+!![]+!![]` or `(!![]+!![])*(!![]+!![])`               |
| 5      | `!![]+!![]+!![]+!![]+!![]`                                       |
### Strings