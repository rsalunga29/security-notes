## Core Windows Processes
Core Windows processes can be seen and understood using Task Manager, a built-in tool by Windows.

Below is a summary of running processes that are considered normal behaviour:
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
## SysInternals
The Sysinternals tools are a compilation of over 70+ Windows-based tools. These tools falls into one of the following categories:
- File and Disk Utilities
- Networking Utilities
- Process Utilities
- Security Utilities
- System Information
- Miscellaneous