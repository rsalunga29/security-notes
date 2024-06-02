Namespaces segregate system resources such as processes, files, and memory away from other namespaces. Every process running on Linux will be assigned two things:
- A namespace
- A Process Identifier (PID)

Namespaces are also the reason how containerization is achieved! Processes can only "see" the process in the same namespace.
## Determine if We're in a Container Process
Using the command `ps aux`, we can list the current processes that are running. The difference in the number of processes is usually a great indicator that we're in a container. However, this is not 100% indicative. There are cases where, ironically, you want the container to be able to interact directly with the host.
## Exploit
Using `cgroups`, we will abuse a situation where the container will share the same namespace as the host OS. You might see this in cases where the container relies on a process running or needs to "plug in" to the host such as the use of debugging tools. In these situations, you can expect to see the host's processes in the container when listing them via `ps aux`.