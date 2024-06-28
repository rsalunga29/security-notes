The lsass.exe (Local Service Authority Subsystem Service) is a process in Windows OS that is responsible for enforcing the security policy on the system. It verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens. It also writes to the Windows Security Log. It's parent process is [wininit.exe](obsidian://open?vault=security-notes&file=Defensive%20Security%2FEndpoint%20Security%2FCore%20Windows%20Processes%2Fwininit.exe).

It creates security tokens for SAM (Security Account Manager), AD (Active Directory), and NETLOGON. It uses authentication packages specified in "HKLM\System\CurrentControlSet\Control\Lsa".
## Adversary Targets
The lsass.exe is a process targeted by adversaries. They commonly use mimikatz to dump user credentials or mimic the process to hide in plain sight.
## What is normal?
**Image Path**: %SystemRoot%\System32\lsass.exe
**Parent Process**: wininit.exe
**Number of Instances**: One
**User Account**: Local System
**Start Time**: Within seconds of boot time
## What is unusual
- A parent process other than wininit.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM