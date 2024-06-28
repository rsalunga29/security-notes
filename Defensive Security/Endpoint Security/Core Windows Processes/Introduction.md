Understanding what is normal behavior within the Windows OS is important to help defenders identify malware and malicious processes running on an endpoint.

Below is a summary of running processes that are considered normal behavior:
- System
- System > smss.exe
- csrss.exe
- wininit.exe
- wininit.exe > services.exe
- wininit.exe > services.exe > svchost.exe
- lsass.exe
- winlogon.exe
- explorer.exe

>Note: ">" symbol represents a parent-child relationship (i.e `System (Parent) > smss.exe (Child)`)

Processes with no depiction of a parent-child relationship should not have a parent process under normal circumstances. Exception to this is the System process which should only have **System Idle Process (0)** as its parent process.

Cybercriminals typically impersonate these processes to avoid detection and hide in plain sight. Read [here](https://www.hexacorn.com/blog/2013/07/04/the-typographical-and-homomorphic-abuse-of-svchost-exe/) and [here](https://www.hexacorn.com/blog/2015/12/18/the-typographical-and-homomorphic-abuse-of-svchost-exe-and-other-popular-file-names/) to know more.