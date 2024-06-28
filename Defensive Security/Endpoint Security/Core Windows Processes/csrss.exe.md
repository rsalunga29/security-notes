The csrss.exe (Client Server Runtime Process) is the user-mode side of the Windows subsystem. This process is always running and is critical to system operation. If this process is terminated by chance, it will result in system failure. This process is responsible for the Win32 console window and process thread creation and deletion. For each instance the following are loaded (along with others):
- csrsrv.dll
- basesrv.dll
- winsrv.dll

The csrss.exe is also responsible for the following:
- making the Windows API available to other processes
- mapping drive letters
- handling the Windows shutdown process.
## What is normal?
**Image Path**: %SystemRoot%\System32\csrss.exe
**Parent Process**: Non-existent process (Created by an instance of smss.exe which self-terminated after)
**Number of Instances**: Two or more
**User Account**: Local System
**Start Time**: Within seconds of boot time for the first two instances (for Session 0 and 1). Start times for additional instances occur as new sessions are created, although only Sessions 0 and 1 are often created.
## What is unusual?
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than "C:\Windows\System32"
- Subtle misspellings to hide rogue processes masquerading as csrss.exe in plain sight
- The user is not the SYSTEM user.