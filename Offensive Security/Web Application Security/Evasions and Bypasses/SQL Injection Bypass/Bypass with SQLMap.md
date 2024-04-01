Whenever we run SQLMap, As part of the initial tests, SQLMap sends a predefined malicious looking payload using a non-existent parameter name (e.g. `?pfov=...`) to test for the existence of a WAF (Web Application Firewall). The following are multiple ways that sqlmap can use to bypass WAFs.
## Anti-CSRF Token Bypass
One of the first line of defense against automation tools is the incorporation of anti-CSRF tokens into all HTTP requests. SQLmap's `--csrf-token` flag can help in bypassing anti-CSRF protection by specifying the token parameter name (e.g `--csrf-token=_csrftoken`).

Additionally, if one of the provided parameters contains any of the infixes (i.e csrf, xsrf, token), the user will be prompted to update the request.
## Unique Value Bypass
In some cases, the web application may only require unique values to be provided inside pre-defined parameters (e.g `?id=1&uid=7389271937219`). For this scenario, the option `--randomize` should be used, pointing the parameter name containing a value which should be randomize before sending the request (e.g `--randomize=uid`).
## Calculated Parameter Bypass
Another similar mechanism is for web applications to expect a proper parameter value to be calculated based on several factors. Most often, one parameter value has to contain a message digest (e.g `h=MD5(id)`) of another parameter. To bypass this, the option `--eval` should be used (e.g `--eval="import hashlib; h=hashlib.md5(id).hexdigest()"`).
## IP Address Concealing
In case where we want to conceal our IP Address or if some web application blacklists our current IP Address, we can use a proxy or Tor. A proxy can be set with the option `--proxy` (e.g `--proxy="socks4://192.168.187.70:33283"`), if we have a list of proxies, we can use the option `--proxy-file` instead.

Using the option `--tor` will have SQLmap use the Tor network. However, if we first wanted to make sure Tor is properly working to avoid unwanted behavior, we can use the `--check-tor` option which makes SQLmap connect to `https://check.torproject.org/` and check the response for the intended results.
## User-agent Blacklisting Bypass
In case of immediate problems (e.g., HTTP error code 5XX from the start) while running SQLMap, one of the first things we should think of is the potential blacklisting of the default user-agent used by SQLMap (e.g. `User-agent: sqlmap/1.4.9 (http://sqlmap.org)`).

This is trivial to bypass with the switch `--random-agent`, which changes the default user-agent with a randomly chosen value from a large pool of values used by browsers.
## Tamper Scripts
The other method that sqlmap uses to bypass WAF/IPS solutions is using "tamper" scripts. Tamper scripts are a special kind of Python scripts written for modifying requests just before being sent to the target, in most cases to bypass some protection.

These scripts can be chained, one after another, within the `--tamper` flag (e.g `--tamper=between,randomcase`). To get a whole list of tamper scripts, use the `--list-tampers` parameter. The most notable tamper scripts are the following:

| Tamper Script             | Description                                                                                                                      |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| 0eunion                   | Replaces instances of UNION with e0UNION                                                                                         |
| base64encode              | Base64-encodes all characters in a given payload                                                                                 |
| between                   | Replaces greater than operator (`>`) with `NOT BETWEEN 0 AND #` and equals operator (`=`) with `BETWEEN # AND #`                 |
| commalesslimit            | Replaces (MySQL) instances like `LIMIT M, N` with `LIMIT N OFFSET M` counterpart                                                 |
| equaltolike               | Replaces all occurrences of operator equal (`=`) with `LIKE` counterpart                                                         |
| halfversionedmorekeywords | Adds (MySQL) versioned comment before each keyword                                                                               |
| modsecurityversioned      | Embraces complete query with (MySQL) versioned comment                                                                           |
| modsecurityzeroversioned  | Embraces complete query with (MySQL) zero-versioned comment                                                                      |
| percentage                | Adds a percentage sign (`%`) in front of each character (e.g. SELECT -> %S%E%L%E%C%T)                                            |
| plus2concat               | Replaces plus operator (`+`) with (MsSQL) function CONCAT() counterpart                                                          |
| randomcase                | Replaces each keyword character with random case value (e.g. SELECT -> SEleCt)                                                   |
| space2comment             | Replaces space character ( ) with comments `/                                                                                    |
| space2dash                | Replaces space character ( ) with a dash comment (`--`) followed by a random string and a new line (`\n`)                        |
| space2hash                | Replaces (MySQL) instances of space character ( ) with a pound character (`#`) followed by a random string and a new line (`\n`) |
| space2mssqlblank          | Replaces (MsSQL) instances of space character ( ) with a random blank character from a valid set of alternate characters         |
| space2plus                | Replaces space character ( ) with plus (`+`)                                                                                     |
| space2randomblank         | Replaces space character ( ) with a random blank character from a valid set of alternate characters                              |
| symboliclogical           | Replaces AND and OR logical operators with their symbolic counterparts (`&&` and `\|\|`)                                         |
| versionedkeywords         | Encloses each non-function keyword with (MySQL) versioned comment                                                                |
| versionedmorekeywords     | Encloses each keyword with (MySQL) versioned comment                                                                             |
## Chunked Transfer Encoding
The Chunked transfer encoding, turned on using the switch `--chunked`, which splits the POST request's body into so-called "chunks." Blacklisted SQL keywords are split between chunks in a way that the request containing them can pass unnoticed.
## HTTP Parameter Pollution
Also known as HPP, is where payloads are split in a similar way as in case of `--chunked` between different same parameter named values (e.g `?id=1&id=UNION&id=SELECT&id=username,password&id=FROM&id=users...`), which are concatenated by the target platform if it supports it.