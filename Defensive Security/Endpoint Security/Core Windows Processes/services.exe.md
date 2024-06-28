The services.exe (Service Control Manager (SCM)) is primarily responsible for handling system services:
- loading services
- interacting with services
- starting or ending services

It maintains a database that can be queried using a Windows built-in utility, `sc.exe`.

It's parent process is [wininit.exe](obsidian://open?vault=security-notes&file=Defensive%20Security%2FEndpoint%20Security%2FCore%20Windows%20Processes%2Fwininit.exe).

Information regarding services is stored in the registry, "HKLM\System\CurrentControlSet\Services". 
## What is normal?
**Image Path**: %SystemRoot%\System32\services.exe
**Parent Process**: wininit.exe
**Number of Instances**: One
**User Account**: Local System
**Start Time**: Within seconds of boot time
## What is unusual?
- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM