The lsass.exe (Local Service Authority Subsystem Service) is a process in Windows OS that is responsible for enforcing the security policy on the system. It verifies users logging on to a Windows computer or server, handles password changes, and creates access tokens. It also writes to the Windows Security Log.

It creates security tokens for SAM (Security Account Manager), AD (Active Directory), and NETLOGON. It uses authentication packages specified in "HKLM\System\CurrentControlSet\Control\Lsa".
## Adversary Targets
The lsass.exe is a process targeted by adversaries. They commonly use mimikatz to dump user credentials or mimic the process to hide in plain sight.