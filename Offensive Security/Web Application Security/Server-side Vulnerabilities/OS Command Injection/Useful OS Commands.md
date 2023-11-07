After identifying an OS command injection vulnerability, it's useful to execute the following initial commands to enumerate the target system:

|Purpose of command|Linux|Windows|
|---|---|---|
|Name of current user|`whoami`|`whoami`|
|Operating system|`uname -a`|`ver`|
|Network configuration|`ifconfig`|`ipconfig /all`|
|Network connections|`netstat -an`|`netstat -an`|
|Running processes|`ps -ef`|`tasklist`|
## Shell Metacharacters
You can also use shell metacharacters to perform the attack.

A number of characters function as command separators, allowing commands to be chained together. The following works on both Windows and Unix-based systems:
- `&`
- `&&`
- `|`
- `||`

The following command separators work only on Unix-based systems:
- `;`
- Newline (`0x0a` or `\n`)

On Unix-based systems, we can also use backticks or the dollar character to perform inline execution of an injected command within the original command:
- <pre>`injected command`</pre>
