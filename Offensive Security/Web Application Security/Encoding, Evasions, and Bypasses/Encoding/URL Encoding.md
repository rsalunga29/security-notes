This table is a character encoding chart that is useful in explaining which characters are “safe” and which characters should be encoded in URLs.
- http://perishablepress.com/stop-using-unsafe-characters-in-urls/

Some commonly encoded characters are:

| Character | Purporse in URL                 | Encoding     |
| --------- | ------------------------------- | ------------ |
| `#`       | Separate anchors                | `%23`        |
| `?`       | Separate query string           | `%3F`        |
| `&`       | Separate query elements         | `%24`        |
| `%`       | Indicates an encoded character  | `%25`        |
| `/`       | Separate domain and directories | `%2F`        |
| `+`       | Indicates a space               | `%2B`        |
| `'`       | Not recommended                 | `%20` or `+` |
