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
### Creating and Applying Sec