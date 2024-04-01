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