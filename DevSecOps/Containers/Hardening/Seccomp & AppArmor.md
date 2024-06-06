## Seccomp
Seccomp is an important security feature of Linux that restricts the actions a program can and cannot do. Seccomp allows you to create and enforce a list of rules of what actions (system calls) the application can make. For example, allowing the application to make a system call to read a file but not allowing it to make a system call to open a new network connection (such as a reverse shell).

These profiles are helpful because they reduce attackers' ability to execute malicious commands whilst maintaining the application's functionality. The following is an example Seccomp profile for a web server:
```json
{
  "defaultAction": "SCMP_ACT_ALLOW",
  "architectures": [
    "SCMP_ARCH_X86_64",
    "SCMP_ARCH_X86",
    "SCMP_ARCH_X32"
  ],
  "syscalls": [
    { "names": [ "read", "write", "exit", "exit_group", "open", "close", "stat", "fstat", "lstat", "poll", "getdents", "munmap", "mprotect", "brk", "arch_prctl", "set_tid_address", "set_robust_list" ], "action": "SCMP_ACT_ALLOW" },
    { "names": [ "execve", "execveat" ], "action": "SCMP_ACT_ERRNO" }
  ]
}
```
This Seccomp profile:
- Allows files to be read and written to
- Allows a network socket to be created
- But does not allow execution (for example, `execve`)
### Creating and Applying Seccomp Profile
To create a Seccomp profile, you can simply create a profile using your favorite text editor. Once created, we can apply it to our container at runtime by using `--security-opt seccomp` for example:
```bash
docker run --rm -it --security-opt seccomp=/home/user/container1/seccomp/profile.json container-name
```
## AppArmor
AppArmor is a similar security feature in Linux because it prevents applications from performing unauthorised actions. However, it works differently from Seccomp because it is not included in the application but in the operating system.

This mechanism is a Mandatory Access Control (MAC) system that determines the actions a process can execute based on a set of rules at the operating system level. To use AppArmor, we first need to ensure that it is installed on our system:
```bash
sudo aa-status
```
The output should show "apparmor module is loaded" to confirm that AppArmor is installed and enabled.
### Creating and Applying AppArmor Profile
To use AppArmor, we must first create a profile using your favorite text editor. For example:
```json
/usr/sbin/httpd {

  capability setgid,
  capability setuid,

  /var/www/** r,
  /var/log/apache2/** rw,
  /etc/apache2/mime.types r,

  /run/apache2/apache2.pid rw,
  /run/apache2/*.sock rw,

  # Network access
  network tcp,

  # System logging
  /dev/log w,

  # Allow CGI execution
  /usr/bin/perl ix,

  # Deny access to everything else
  /** ix,
  deny /bin/**,
  deny /lib/**,
  deny /usr/**,
  deny /sbin/**
}
```

This profile allows an Apache web server to:
- Can read files located in `/var/www/`, `/etc/apache2/mime.types` and `/run/apache2`. 
- Read & write to `/var/log/apache2`.
- Bind to a TCP socket for port 80 but not other ports or protocols such as UDP.
- Cannot read from directories such as `/bin`, `/lib`, `/usr`.

Next, we will need to import this profile into the AppArmor program by:
```bash
sudo apparmor_parser -r -W /home/user/container1/apparmor/profile.json
```

Next, we can apply it to our container at runtime by using the `--security-opt apparmor` flag with the location of the AppArmor profile. For example:
```bash
docker run --rm -it --security-opt apparmor=/home/user/container1/apparmor/profile.json container-name
```
## Difference Summary
- AppArmor determines what resources an application can access (i.e., CPU, RAM, Network interface, filesystem, etc) and what actions it can take on those resources.
- Seccomp is within the program itself, which restricts what system calls the process can make (i.e. what parts of the CPU and operating system functions).

It's important to note that it is not a "one or the other" case. Seccomp and AppArmor can be combined to create layers of security for a container.