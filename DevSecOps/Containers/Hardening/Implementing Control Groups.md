Control Groups (also known as cgroups) are a feature of the Linux kernel that facilitates restricting and prioritising the number of system resources a process can utilise.

In the context of Docker, implementing cgroups helps achieve isolation and stability. Because cgroups can be used to determine the number of (or prioritise) resources a container uses, this helps prevent faulty or malicious containers from exhausting a system.

This behaviour is not enabled by default on Docker and must be enabled per container when starting the container. To specify the limit of resources a container can use, the following commands must be issued:
```bash
docker run -it --cpus="1" --memory="20m" container-name
```
You can also update this setting once the container is running. To do so, use:
``