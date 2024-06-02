## What is Capabilities?
Capabilities in Linux are root permissions given to certain processes or executables within the Linux kernel. These privileges allow for the granular assignment of privileges. These capabilities determine what permissions a Docker container has to the operating system. Docker containers can run in two modes:
- **User (Normal) mode**: Only restricted to Docker engine.
- **Privileged mode**: Able to access and run command on host OS as root.
