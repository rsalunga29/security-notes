The winlogin.exe (Windows Logon) is responsible for handling the Secure Authentication Sequence (SAS). It is the ALT+CTRL+DELETE key combination users press to enter their username & password.

This process is also responsible for loading the user profile. It loads the user's NTUSER.DAT into HKCU, and userinit.exe loads the user's shell.

This process is also responsible for locking the screen and running the screensaver, among other functions.
## What is normal?
**Image Path**: %SystemRoot%\System32\winlogon.exe
**Parent Process**: Non-existent process (Created by an instance of smss.exe which self-terminated after)
**Number of Instances**: One or more
**User Account**: Local System
**Start Time**: Within seconds of boot time for the first instance (for Session 1). Additional instances occur as new sessions are created, typically through Remote Desktop or Fast User Switching logons.
## What is unusual?
- An actual parent process. (smss.exe calls this process and self-terminates)
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- Not running as SYSTEM
- Shell value in the registry other than explorer.exe