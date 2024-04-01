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
As we have seen with Booleans, it is possible to extract the TRUE and FALSE strings but, what if we want to generate the `alert` string? We need to generate each character separately and then put them together.

As such:
- `[![]+[]][+[]][++[[]][+[]]]` generates "a" from `false`.
- `[![]+[]][+[]][++[[]][+[]]+[++[[]][+[]]][+[]]]` generates "l" from `false`.
- `[![]+[]][+[]][++[[]][+[]]+[++[[]][+[]]][+[]]+[++[[]][+[]]][+[]]+[++[[]][+[]]][+[]]]` generates "e" from `false`.
- `[!![]+[]][+[]][+!![]]` generates "r" from `true`.
- `[!![]+[]][+[]][+[]]` generates "t" from `true`.

Combining it all together, we get the word `alert`:
```js
[![]+[]][+[]][++[[]][+[]]]+[![]+[]][+[]][++[[]][+[]]+[++[[]][+[]]][+[]]]+[![]+[]][+[]][++[[]][+[]]+[++[[]][+[]]][+[]]+[++[[]][+[]]][+[]]+[++[[]][+[]]][+[]]]+[!![]+[]][+[]][+!![]]+[!![]+[]][+[]][+[]]
```
### JJencode
JJencode is the way by which Hasegawa encodes JavaScript code using only symbols. It uses a customizable global variable name and from that encodes the payload. We can use [Hasegawa's website](https://utf-8.jp/public/jjencode.html) to generate JJencode.

For example:
```js
$=~[];$={___:++$,$$$$:(![]+"")[$],__$:++$,$_$_:(![]+"")[$],_$_:++$,$_$$:({}+"")[$],$$_$:($[$]+"")[$],_$$:++$,$$$_:(!""+"")[$],$__:++$,$_$:++$,$$__:({}+"")[$],$$_:++$,$$$:++$,$___:++$,$__$:++$};$.$_=($.$_=$+"")[$.$_$]+($._$=$.$_[$.__$])+($.$$=($.$+"")[$.__$])+((!$)+"")[$._$$]+($.__=$.$_[$.$$_])+($.$=(!""+"")[$.__$])+($._=(!""+"")[$._$_])+$.$_[$.$_$]+$.__+$._$+$.$;$.$$=$.$+(!""+"")[$._$$]+$.__+$._+$.$+$.$$;$.$=($.___)[$.$_][$.$_];$.$($.$($.$$+"\""+$.$_$_+(![]+"")[$._$_]+$.$$$_+"\\"+$.__$+$.$$_+$._$_+$.__+"(\\\"\\"+$.__$+$.__$+$.___+$.$$$_+(![]+"")[$._$_]+(![]+"")[$._$_]+$._$+"\\\"\\"+$.$__+$.___+")"+"\"")())();
```
### AAencode
A different approach is with AAencode. It is inspired by Japanese style emoticons. We can use [Hasegawa's website](https://utf-8.jp/public/aaencode.html) to generate AAencode.

For example:
```js
ﾟωﾟﾉ= /｀ｍ´）ﾉ ~┻━┻   //*´∇｀*/ ['_']; o=(ﾟｰﾟ)  =_=3; c=(ﾟΘﾟ) =(ﾟｰﾟ)-(ﾟｰﾟ); (ﾟДﾟ) =(ﾟΘﾟ)= (o^_^o)/ (o^_^o);(ﾟДﾟ)={ﾟΘﾟ: '_' ,ﾟωﾟﾉ : ((ﾟωﾟﾉ==3) +'_') [ﾟΘﾟ] ,ﾟｰﾟﾉ :(ﾟωﾟﾉ+ '_')[o^_^o -(ﾟΘﾟ)] ,ﾟДﾟﾉ:((ﾟｰﾟ==3) +'_')[ﾟｰﾟ] }; (ﾟДﾟ) [ﾟΘﾟ] =((ﾟωﾟﾉ==3) +'_') [c^_^o];(ﾟДﾟ) ['c'] = ((ﾟДﾟ)+'_') [ (ﾟｰﾟ)+(ﾟｰﾟ)-(ﾟΘﾟ) ];(ﾟДﾟ) ['o'] = ((ﾟДﾟ)+'_') [ﾟΘﾟ];(ﾟoﾟ)=(ﾟДﾟ) ['c']+(ﾟДﾟ) ['o']+(ﾟωﾟﾉ +'_')[ﾟΘﾟ]+ ((ﾟωﾟﾉ==3) +'_') [ﾟｰﾟ] + ((ﾟДﾟ) +'_') [(ﾟｰﾟ)+(ﾟｰﾟ)]+ ((ﾟｰﾟ==3) +'_') [ﾟΘﾟ]+((ﾟｰﾟ==3) +'_') [(ﾟｰﾟ) - (ﾟΘﾟ)]+(ﾟДﾟ) ['c']+((ﾟДﾟ)+'_') [(ﾟｰﾟ)+(ﾟｰﾟ)]+ (ﾟДﾟ) ['o']+((ﾟｰﾟ==3) +'_') [ﾟΘﾟ];(ﾟДﾟ) ['_'] =(o^_^o) [ﾟoﾟ] [ﾟoﾟ];(ﾟεﾟ)=((ﾟｰﾟ==3) +'_') [ﾟΘﾟ]+ (ﾟДﾟ) .ﾟДﾟﾉ+((ﾟДﾟ)+'_') [(ﾟｰﾟ) + (ﾟｰﾟ)]+((ﾟｰﾟ==3) +'_') [o^_^o -ﾟΘﾟ]+((ﾟｰﾟ==3) +'_') [ﾟΘﾟ]+ (ﾟωﾟﾉ +'_') [ﾟΘﾟ]; (ﾟｰﾟ)+=(ﾟΘﾟ); (ﾟДﾟ)[ﾟεﾟ]='\\'; (ﾟДﾟ).ﾟΘﾟﾉ=(ﾟДﾟ+ ﾟｰﾟ)[o^_^o -(ﾟΘﾟ)];(oﾟｰﾟo)=(ﾟωﾟﾉ +'_')[c^_^o];(ﾟДﾟ) [ﾟoﾟ]='\"';(ﾟДﾟ) ['_'] ( (ﾟДﾟ) ['_'] (ﾟεﾟ+(ﾟДﾟ)[ﾟoﾟ]+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ (ﾟｰﾟ)+ (ﾟΘﾟ)+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ ((ﾟｰﾟ) + (ﾟΘﾟ))+ (ﾟｰﾟ)+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ (ﾟｰﾟ)+ ((ﾟｰﾟ) + (ﾟΘﾟ))+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ ((o^_^o) +(o^_^o))+ ((o^_^o) - (ﾟΘﾟ))+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ ((o^_^o) +(o^_^o))+ (ﾟｰﾟ)+ (ﾟДﾟ)[ﾟεﾟ]+((ﾟｰﾟ) + (ﾟΘﾟ))+ (c^_^o)+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟｰﾟ)+ ((o^_^o) - (ﾟΘﾟ))+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ (ﾟΘﾟ)+ (c^_^o)+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ (ﾟｰﾟ)+ ((ﾟｰﾟ) + (ﾟΘﾟ))+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ ((ﾟｰﾟ) + (ﾟΘﾟ))+ (ﾟｰﾟ)+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ ((ﾟｰﾟ) + (ﾟΘﾟ))+ (ﾟｰﾟ)+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟΘﾟ)+ ((ﾟｰﾟ) + (ﾟΘﾟ))+ ((ﾟｰﾟ) + (o^_^o))+ (ﾟДﾟ)[ﾟεﾟ]+(ﾟｰﾟ)+ ((o^_^o) - (ﾟΘﾟ))+ (ﾟДﾟ)[ﾟεﾟ]+((ﾟｰﾟ) + (ﾟΘﾟ))+ (ﾟΘﾟ)+ (ﾟДﾟ)[ﾟoﾟ]) (ﾟΘﾟ)) ('_');
```
### JSFuck


To encode use https://jsfuck.com/.