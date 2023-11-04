Some applications only allow inputs that match, a whitelist of allowed values. The filter will look for a match at the beginning or within the provided input. You may be able to bypass this filter by exploiting inconsistencies in URL parsing.

The URL specification contains a number of features that are likely overlooked when URLs implement parsing and validation using this method:
- You can embed credentials in a URL before the hostname by using the `@` character.
```txt
https://username:password@target-host
```
- You can use the `#` character to indicate a URL fragment
```txt
https://evil-host#target-host
```
- You can leverage the DNS naming hierarchy to place required input into fully-qualified DNS name that you control
```txt
https://target-host.evil-host
```
- You can URL-encode characters to confuse the URL-parsing code.