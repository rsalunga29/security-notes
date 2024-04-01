## Mod Security Rules
## AWS WAF
### Bypass with Line Folding
Web servers like Node.js, Flask and many others sometimes encounter a phenomenon known as "line folding." Line folding refers to the practice of splitting long header values using the characters `\x09` (tab) and `\x20` (space) into multiple lines for readability. However, this behavior can lead to compatibility issues and potential security vulnerabilities.