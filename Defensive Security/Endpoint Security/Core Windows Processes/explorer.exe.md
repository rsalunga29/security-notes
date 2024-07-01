The explorer.exe (Windows Explorer) gives the user access to their folders and files. It also provides functionality for other features, such as the Start Menu and Taskbar.

As mentioned in the [winlogon.exe](obsidian://open?vault=security-notes&file=Defensive%20Security%2FEndpoint%20Security%2FCore%20Windows%20Processes%2Fwinlogon.exe) page, the winlogon.exe runs userinit.exe, which launches the value in "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell", it then exits after spawning explorer.exe, hence the parent process for explorer.exe is non-existent.

There will be many child processes for explorer.exe.
## What is normal?
**Image Path**: %SystemRoot%\explorer.exe
**Parent Process**: Non-existent process (Created by an instance of userinit.exe which self-terminated after)
**Number of Instances**: One or more per interactively logged-in user
**User Account**:  Logged-in user(s)
**Start Tim**e: First instance when the first interactive user logon session begins
## What is unusual?
- An actual parent process. (userinit.exe calls this process and exits)
- Image file path other than C:\Windows
- Running as an unknown user
- Subtle misspellings to hide rogue processes in plain sight
- Outbound TCP/IP connections