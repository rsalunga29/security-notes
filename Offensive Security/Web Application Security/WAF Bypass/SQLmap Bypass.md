Whenever we run SQLMap, As part of the initial tests, SQLMap sends a predefined malicious looking payload using a non-existent parameter name (e.g. `?pfov=...`) to test for the existence of a WAF (Web Application Firewall). The following are multiple ways that sqlmap can use to bypass WAFs.
## User-agent Blacklisting Bypass
In case of immediate problems (e.g., HTTP error code 5XX from the start) while running SQLMap, one of the first things we should think of is the potential blacklisting of the default user-agent used by SQLMap (e.g. `User-agent: sqlmap/1.4.9 (http://sqlmap.org)`).

This is trivial to bypass with the switch `--random-agent`, which changes the default user-agent with a randomly chosen value from a large pool of values used by browsers.
## Tamper Scripts
The other method that sqlmap uses to bypass WAF/IPS solutions is using "tamper" scripts. Tamper scripts are a special kind of Python scripts written for modifying requests just before being sent to the target, in most cases to bypass some protection.