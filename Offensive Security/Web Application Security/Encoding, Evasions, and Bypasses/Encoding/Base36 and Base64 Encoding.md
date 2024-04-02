## Base 36 Encoding Scheme
Its the most compact, case-insensitive, alphanumerical system using ASCII characters. In fact, the schemes alphabet contains all digits [0-9] and Latin letters [A-Z].

It is used in many real world scenarios, such as:
- Reddit uses Base36 for identifying both posts and comments.
- URL shortening services like TinyURL uses Base36 integer as compact, alphanumeric ids.

Another example is if we want to convert **OHPE** from Base36 to decimal, there are different implementations in many programming languages.

In PHP, the `base_convert()` function is used to convert numbers:
```php
# OHPE in Base 10 is:
<?=base_convert("OHPE",36,10);?>
```

While in JavaScript, two functions are being used:
```js
(1142690.toString(36)
1142690..toString(36) #encode
parseInt("ohpe",36)   #decode
```
## Base64 Encoding Scheme
Base64 is one of the most widespread binary-to-text encoding schemes to date. It was designed to allow binary data to be represented as ASCII string text.

The alphabet of the Base64 encoding scheme is composed of digits [0-9] and Latin letters, both upper and lower case [a-zA-Z], For a total of 62 values. To complete the character set to 64 there are the plus (`+`) and slash (`/`) characters.

The algorithm divides the message into groups of 6 bits* and then converts each group, with the respective ASCII character, following the conversion table:
![[base64-encoding-algo-1.png]]
![[base64-encoding-algo-2.png]]

Thats why the allowed characters are 64 (2 raised to 6th power = 64)
- If the latest group is **null** (000000) the respective encoding value is **=**.
- If the trailing **null groups** are two, then will be encoded as `==`.

Due to its popularity, there are many encoding / decoding implementations of Base64 in many programming languages.

In PHP, the `base64_encode()` and `base64_decode()` functions are used:
```php
<?=base64_encode('encode this string')?> //encode
<?=base64_decode('ZW5jb2RlIHRoaXMgc3RyaW5n')?> //decode
```

While in JavaScript, many browsers can handle Base64 natively through `btoa()` and `atob()` functions.
```js
window.btoa('encode this string'); //encode
window.atob('ZW5jb2RlIHRoaXMgc3RyaW5n'); //decode
```