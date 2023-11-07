After identifying an OS command injection vulnerability, it's useful to execute the following initial commands to enumerate the target system:

|Purpose of command|Linux|Windows|
|---|---|---|
|Name of current user|`whoami`|`whoami`|
|Operating system|`uname -a`|`ver`|
|Network configuration|`ifconfig`|`ipconfig /all`|
|Network connections|`netstat -an`|`netstat -an`|
|Running processes|`ps -ef`|`tasklist`|

You can also use the following