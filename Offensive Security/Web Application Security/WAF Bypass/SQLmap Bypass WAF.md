Whenever we run SQLMap, As part of the initial tests, SQLMap sends a predefined malicious looking payload using a non-existent parameter name (e.g. `?pfov=...`) to test for the existence of a WAF (Web Application Firewall). The following are multiple ways that sqlmap can use to bypass WAFs.
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
