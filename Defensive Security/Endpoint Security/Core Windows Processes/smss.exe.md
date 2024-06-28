The smss.exe (Session Manager Subsystem) also known as Windows Session Manager, is responsible for creating new sessions. It is the first child instance and user-mode process started by the kernel. It's parent process is [System](obsidian://open?vault=security-notes&file=Defensive%20Security%2FEndpoint%20Security%2FCore%20Windows%20Processes%2FSystem).

This process starts the kernel and user modes of the Windows subsystem which includes win32k.sys (kernel mode), winsrv.dll (user mode), and csrss.exe (user mode). Read more about the NT Architecture [here](https://en.wikipedia.org/wiki/Architecture_of_Windows_NT).
## The Process
Smss.exe starts csrss.exe (Windows subsystem) and wininit.exe in Session 0 (An isolated Windows session for the OS). It also starts the csrss.exe and winlogon.exe (the Windows Logon Manager) in Session 1 (User session).

Basically, the first child instance creates child instances in new sessions. This is done by smss.exe copying itself into the new session and self-terminating.

Any other subsystem listed in the `Required` value of "HKLM\System\CurrentControlSet\Control\Session Manager\Subsystems" is also launched.

SMSS is also responsible for creating environment variables and virtual memory paging files.
## What is normal?
**Image Path**:  %SystemRoot%\System32\smss.exe
**Parent Process**:  System
**Number of Instances**:  One master instance and child instance per session. The child instance exits after creating the session.
**User Account**:  Local System
**Start Time**:  Within seconds of boot time for the master instance
## What is unusual?
- A different parent process other than System (4)
- The image path is different from C:\Windows\System32
- More than one running process. (children self-terminate and exit after each new session)
- The running User is not the SYSTEM user
- Unexpected registry entries for Subsystem