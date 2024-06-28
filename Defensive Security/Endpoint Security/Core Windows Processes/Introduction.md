Understanding what is normal behavior within a Windows operation system is important to help you identify malicious processes running on an endpoint.

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