## Overview
- Perform a thorough Black Box Web Penetration Test against web applications of Tera Host.
- Tests must be conducted on all hosts, domains, and subdomains in the scope.
- Report any vulnerability and any working exploit.
- Full exploitation of all every identified vulnerability is a must. Simple error messages or payloads will not be counted.
## Scope
- Dedicated Web Server: 10.100.13.37 (also a DNS server)
- Domain: \*.terahost.exam (all subdomains)
- Dedicated Web Servers: 10.100.13.33, 10.100.13.34
## Passing Conditions
- Report content of `/usr/local/etc/exam/pass`
- Reverse shells on two localhost services that reside on 10.100.13.34
>Note: These are necessary but **insufficient**.