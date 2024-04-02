Unicode (aka ISO/IEC 10646 Universal Character Set) is the character encoding standard created to enable people around the world to use computers in any language. It supports all the world's writing systems. It can also expose web applications to possible attacks, like bypassing security filters for example.

There are three ways to map Unicode character points:
- UTF-8
- UTF-16
- UTF-32
> Note: UTF means Unicode Transformation Format and the trailing number indicates the number of bits to represent code points.

Each UTF has different representation. The following table shows a sample message encoded in the three different UTF formats.

| Character | Unicode | UTF-8       | UTF-16    | UTF-32   |
| --------- | ------- | ----------- | --------- | -------- |
| `I`       | U+0049  | 49          | 0049      | 00000049 |
| `♥`       | U+2665  | E2 99 A5    | 2665      | 00002665 |
| `🍻`      | U+1F37B | F0 9F 8D BB | D83C DF7B | 0001F37B |
Additionally, the following table shows how Unicode characters are handled through different implementations like URLs, HTML, JavaScript, etc...

| Character | Unicode | URL-Encoding   | HTML Entity                           | JavaScript, JSON, Java |
| --------- | ------- | -------------- | ------------------------------------- | ---------------------- |
| `I`       | U+0049  | `%49`          | `&#73;` or `&#x49;`                   | `\u0049`               |
| `♥`       | U+2665  | `%E2%99%A5`    | `&hearts;` or `&#9829;` or `&#x2665;` | `\u2665`               |
| `🍻`      | U+1F37B | `%F0%9F%8D%8B` | `&#127867;` or `&#x1F37B;`            | `\uD83C\uDF7B`         |
## Homoglyph
In typography, a homoglyph is one or two or more characters, or glyphs, with shapes that either appear identical or cannot be differentiated by quick visual inspection.

Additional classification includes:
- Homograph - a word that looks the same as another word.
- Homogliph - a look-alike character used to create homographs.
### Visual Spoofing
One of the possible attacks with Unicode is called, **Visual Spoofing**.
![[visual-spoofing-1.png]]
![[visual-spoofing-2.png]]

If we analyze the character code points of the string, the differences are evident, but for a human this is not so obvious. These kind of characters are known as [confusable](https://util.unicode.org/UnicodeJsps/confusables.jsp).

To speed the homographs generation, the [Homoglyph Attack Generator](https://www.irongeek.com/homoglyph-attack-generator.php) can be used instead.

This type of attacks are being used in the real world:
- [Use of Punycode and Homoglyph Attacks to Obfuscate URLs for Phishing](https://www.irongeek.com/i.php?page=security/out-of-character-use-of-punycode-and-homoglyph-attacks-to-obfuscate-urls-for-phishing)
- [Creative usernames and Spotify account hijacking](https://engineering.atspotify.com/2013/06/creative-usernames/)
- Bypass anti XSS and SQLi filters

As such, many applications implements validation and processes to convert
