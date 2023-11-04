Some applications only allow inputs that match, a whitelist of allowed values. The filter will look for a match at the beginning or within the provided input. You may be able to bypass this filter by exploiting inconsistencies in URL parsing.

The URL specification contains a number of features that are likely overlooked when URLs implement parsing and validation using this method:
- You can embed credentials in a URL before the hostname by using the `@` character.
```txt
https://target-host:fakepassword@expected-host
```
```txt
https://target-host@expected-host/target-url
```
- You can use the `#` character to indicate a URL fragment
```txt
https://target-host#expected-host
```
- You can leverage the DNS naming hierarchy to place required input into fully-qualified DNS name that you control
```txt
https://expected-host.evil-host
```
- You can URL-encode characters to confuse the URL-parsing code. This is useful specially if the code that implements the filter handles URL-encoded characters differently compared to the code that performs the backend HTTP request.
- You can try double URL-encoding characters, some servers recursively URL-decode the input they receive, which may lead to further discrepancies.

Often times, multiple anti-SSRF filters are deployed, you can combine the techniques described above to bypass the filters and exploit the SSRF vulnerabilities.
## Abusing URL Parsers to Exploit SSRFs
![A new era for SSRF - Exploiting URL Parsers](https://www.youtube.com/watch?v=D1S-G8rJrEk)