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
WAFs usually work in passive mode, reactive mode, or sometimes both.