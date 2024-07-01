The svchost.exe (Service Host) is responsible for hosting and managing Windows services. It's parent process is [services.exe](obsidian://open?vault=security-notes&file=Defensive%20Security%2FEndpoint%20Security%2FCore%20Windows%20Processes%2Fservices.exe).

The services running in this process are implemented as DLLs. The DLL to implement is stored in the registry for the service under the `Parameters` subkey in `ServiceDLL`. The full path is "HKLM\SYSTEM\CurrentControlSet\Services\SERVICE_NAME\Parameters". To view this information from within Process Hacker:
1. Right-click the svchost.exe process.
2. Go to "Services" and click "Go to service".
3. Right-click the service and select "Properties".

Legitimate svchost.exe processes is called with the key identifier / parameter `-k`. For example:
`C:\Windows\system32\svchost.exe -k DcomLaunch -p`.
## What is normal?
**Image Path**: %SystemRoot%\System32\svchost.exe
**Parent Process**: services.exe
**Number of Instances**: Many
**User Account**: Varies (SYSTEM, Network Service, Local Service) depending on the svchost.exe instance. In Windows 10, some instances run as the logged-in user.
**Start Time**: Typically within seconds of boot time. Other instances of svchost.exe can be started after boot.
## What is unusual?
- A parent process other than services.exe
- Image file path other than C:\Windows\System32
- Subtle misspellings to hide rogue processes in plain sight
- The absence of the -k parameter