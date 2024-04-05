A web application firewall (WAF) is a firewall that monitors, filters and blocks malicious HTTP traffic to a website or API.
## WAF Rules
WAFs uses regex to define the rules which define which input is good or bad for the website or API. The meaning/context given to the rules defines the mode by which a WAF should behave - it can be whitelisting or blacklisting.
### Whitelisting Mode
A WAF in whitelisting mode only allows what is explicitly defined in the rules.

As such, whitelisting mode is the best mode, however, customizing the rules is not an easy task. Furthermore, whitelisting more is prone to false positives, which is the reason it is very common to find WAFs deployed using blacklisting mode.
### Blacklisting Mode
A WAF blacklisting mode allows anything except what is explicitly denied in the rules.

The blacklisting mode is a collection of well-known attacks. WAF producers put together a list of well-known payloads and attack vectors that are used to exploit the most common vulnerabilities.

The main problem with this approach is that there are multiple ways to reach the same goal, meaning, a small change in the attack payload means [bypassing the WAF](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FEncoding%2C%20Evasions%2C%20and%20Bypasses%2FWAF%20Bypass).
## Detection and Fingerprinting
WAFs usually work in passive mode, reactive mode, or sometimes both. WAF systems typically leave several footprints or signatures of their presence, allowing attackers to detect which WAF is in place.
### Cookie Values
Some WAF systems reveal their presence by releasing cookies during HTTP communications. For example:
- **Citrix Netscaler** uses cookies such as `ns_af`, `citrix_ns_id`, or `NSC_` in HTTP responses.
- **F5 BIG-IP ASM** uses cookies starting with `TS` and followed by a string that respect the following regex: `^TS[a-zA-Z0-9]{3,6}`.
- **Barracuda** uses `barra_counter_session` and `BNI__BARRACUDA_LB_COOKIE`.
### Header Rewrite
Some WAFS rewrite the HTTP headers, such as modifying the `Server `header (which is pretty common) to deceive attackers.

There are also times where, WAFs completely remove the HTTP `Server` header in the response.

**HTTP response header for non-hostile request**
```http
HTTP/1.1 200 OK
Server: Apache (Unix)
Content-Type: text/html
...
```
**HTTP response header for hostile request**
```http
HTTP/1.1 404 Not Found
Server: Netscape-Enterprise/6.1
Content-Type: text/html
...
```
### HTTP Response Code and Body
Some WAFs modify the HTTP response codes and body content if the request is hostile. For example:
**mod_security**
- Uses `406 Not Acceptable` header.
- Shows an error message with title **Not Acceptable!** and description containing "This error was generata"

**AQTRONIX WebKnight**
- AA