The wininit.exe (Windows Initialization Process) is responsible for launching the following within Session 0:
- services.exe (Service Control Manager)
- lsass.exe (Local Security Authority)
- lsaiso.exe

> Note: lsaiso.exe is a process associated with **Credential Guard and KeyGuard**. You will only see this process if Credential Guard is enabled.

The wininit.exe is another critical Windows process that runs in the background, along with its child processes.
## What is normal?
**Image Path**:  %SystemRoot%\System32\wininit.exe
**Parent Process**:  Created by an instance of smss.exe
**Number of Instances**:  One
**User Account**:  Local System
**Start Time**:  Within seconds of boot time
## What is unusual?
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Multiple running instances
- Not running as SYSTEM