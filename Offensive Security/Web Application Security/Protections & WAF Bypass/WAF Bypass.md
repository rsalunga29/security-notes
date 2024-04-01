## Mod Security Rules
## AWS WAF
### Bypass with Line Folding
Web servers like Node.js, Flask and many others sometimes encounter a phenomenon known as "line folding." Line folding refers to the practice of splitting long header values using the characters `\x09` (tab) and `\x20` (space) into multiple lines for readability. However, this behavior can lead to compatibility issues and potential security vulnerabilities.

For example, the header `1337: Value\r\n\t1337` in the following request will be interpreted as `1337: Value\t1337` in the Node.js server:
```http
GET / HTTP/1.1
Host: target.com
1337: Value
    1337
Connection: close
```